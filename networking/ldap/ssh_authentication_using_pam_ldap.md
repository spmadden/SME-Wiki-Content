## SSH Authentication using pam_ldap

You will have to configure /etc/ldap.conf to connect to your local ldap server. A basic configuration is shown below:

      ssl no
      tls_cacertdir /etc/openldap/cacerts
      pam_password md5
      timelimit 120
      bind_timelimit 120
      idle_timelimit 3600
      # here is where we configure the connection settings
      base [dc=example,dc=com]
      uri ldap://[server]/
      binddn [cn=proxyuser,dc=example,dc=com]
      bindpw secret

Note: BindDN and BindPW are optional

Once LDAP is configured, use a ldap client to connect (using the Directory Manager account you created at startup) and create a user. I like both Lima and PHPLdapAdmin for this purpose.

Note: If you're getting some weird authentication errors in /var/log/secure that look like the following:

    Jan 27 20:46:39 localhost sshd[5169]: pam_ldap: error trying to bind as user "uid={uid},ou=People, dc=seanmadden,dc=net" (Invalid credentials)
    Jan 27 20:46:39 localhost sshd[5169]: pam_unix(sshd:auth): check pass; user unknown

Then you'll need to modify your name service switcher file ( /etc/nsswitch.conf ) to look like the following:

      # Example:
      #passwd:    db files nisplus nis
      #shadow:    db files nisplus nis
      #group:     db files nisplus nis
      
      passwd:     files ldap
      shadow:     files ldap
      group:      files

You will add 'ldap' to the end of the passwd and shadow lines. Add it to the end of the group line for group resolution as well. Then restart the nss service by issuing

    /sbin/service nscd restart

It should be functional at this point.

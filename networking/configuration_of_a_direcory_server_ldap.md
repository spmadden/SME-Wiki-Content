## Configuration of a Directory Server (LDAP)

Fedora's Directory server project (formerly 'fedora directory') has been renamed to 389 (<http://directory.fedoraproject.org>). As such, the packages required have been renamed to 389-\* packages.

Install the base of what you're going to need for the server.

    sudo yum install 389-ds --enablerepo=updates-testing

Then run

    sudo setup-ds-admin.pl

It will prompt you for a number of settings, typically it's okay to just keep hitting 'enter' until it prompts you for a password. This password will be the DirectoryManager user. The global administrator for the domain.

Once the script has finished, the server should be functional.

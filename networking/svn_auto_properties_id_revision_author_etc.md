## SVN Auto-Properties

### Initial configuration

This is known as 'SVN keyword substitution'.

The idea is thus:

You have a list of supported keywords and their format:

    Date/LastChangedDate : $Date$ => $Date: 2006-07-22 21:42:37 -0700 (Sat, 22 Jul 2006) $
    Revision/Rev/LastChangedRevision : $Rev$ => $Rev: 144 $
    Author/LastChangedBy : $Author$ => $Author: bob $
    HeadURL/URL : $URL$ => $URL: http://svn.seanmadden.net/repository/trunk/README $
    Id : $Id$ => $Id: calc.c 148 2006-07-28 21:30:43Z bill $

SVN will automatically search and replace these in text files that have the '<svn:keywords>' property set to which keywords you want to replace. For example:

    svn propset svn:keywords "Id Revision" README

Will tell SVN to replace Id and Revision keywords with their format in the README file.

The problem with this setup is that SVN will not automatically set this property on files unless you tell it to. Thankfully, this is a fairly simple fix (At least in Fedora 12)

When you install subversion, a directory is created in /etc called subversion (/etc/subversion). Chances are, this will be empty.

Create a file in here called 'config' with the following directives:

    [miscellany]
    enable-auto-props = yes

    [auto-props]
    *.c = svn:keywords=Revision Id

The enable-auto-props directive tells SVN to start automatically applying properties while the \[auto-props\] group lists matching rules to apply to. In this case, for all .C files, apply the <SVN:Keywords> property and set it to "Revision Id".

This should be all that is required to get the system set up and running.

Note: you should customize the auto-props rules to suit the environment and files you want to be propertied.

### Applying to existing repositories

Now that we have SVN setup to automatically apply these properties to new files, what say we get our current repositories setup with this property, yes?

It's a pretty straightforward process that can be accomplished using some shell-fu with the 'find' command.

To recursively apply this property to every file in a repository, navigate to a current working copy and run the following:

    svn update 
    find . -exec svn propset svn:keywords "[keywords]" {} ';'

Make sure to replace \[keywords\] with the keywords (listed above) that you would like to be replaced.

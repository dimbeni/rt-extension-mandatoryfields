% RT-Extension-MandatoryFields - Enforce users to fill standard fields when creating a ticket


This RT Extension enforces users to fill standard fields defined in RT site configuration file when creating a ticket via the web interface.


# Installation

To install this extension, run the following commands:

~~~~~~~ {.bash}
perl Makefile.PL
make
make test
make install
~~~~~~~


# Configuration

To make this extension active register it to in RT site configuration file located in `RT_HOME/etc/RT_SiteConfig.pm` where `RT_HOME` is the path to your RT installation.

~~~~~~~ {.perl}
Set(@Plugins,qw(RT::Extension::MandatoryFields));
~~~~~~~

To enforce users to fill the standard fields add them to `%MandatoryFields`:

~~~~~~~ {.perl}
Set(%MandatoryFields, (
    'Requestors' => 'true',
    'Cc' => 'true',
    'AdminCc' => 'true',
    'Subject' => 'true',
    'Content' => 'true',
    'Attach' => 'true',
    'Status' => 'true',
    'Owner' => 'true'
));
~~~~~~~

Mark a mandatory field with 'true', otherwise 'false'.

Note: There are more than one way to create a new ticket. The default way is 'Create', but there are 'QuickCreate' on the home page and 'SelfService' for unpreviledged users, too. This extension handles them all. If a formular doesn't include one of the fields marked as mandatory (set to 'true' in the configuration) it will be ignored. Don't get confused, if you set a mandatory field that won't show up on the web interface. The table below gives you a short summarize which formular supports which mandatory field.

Field         Mandatory Per Default    Create      QuickCreate         SelfService
------------  -----------------------  ----------  ------------------  ---------------------
Requestors    no                       included    included            included
Cc            no                       included    **not** included    included
AdminCc       no                       included    **not** included    **not** included
Subject       no                       included    included            included
Content       no                       included    included            included
Attach        no                       included    **not** included    included
Status        no                       included    **not** included    **not** included
Owner         no                       included    included            **not** included

After all your new configuration will take effect after restarting your RT environment:

~~~~~~~ {.bash}
rm -rf RT_HOME/var/mason_data/obj/* && service apache2 restart
~~~~~~~

This is an example for deleting the mason cache and restarting the Apache HTTP web server on a Debian based operating system.


# Author

Benjamin Heisig, <bheisig@synetics.de>


# Support and Documentation

You can find documentation for this module with the `perldoc` command.

~~~~~~~ {.bash}
perldoc RT::Extension::MandatoryFields
~~~~~~~


# Bugs

Please report any bugs or feature requests to the [author](#author).


# Acknowledgements

This extension is a fork of `RT::Extension::MandatorySubject` written by Emmanuel Lacour.

Special thanks to the *synetics GmbH*, <http://i-doit.org/> for initiating and supporting this project!


# Copyright and License

Copyright (C) 2011 Benjamin Heisig, <bheisig@synetics.de>

This program is free software; you can redistribute it and/or modify it under the same terms as Perl itself.

Request Tracker (RT) is Copyright Best Practical Solutions, LLC.

**Performing Name Resolution with host**

_host_ is an elementary DNS lookup utility that works on the same principles as the _dig_ command in terms of nameserver determination. This tool produces lesser data in the output by default; however, you can add the -v option for verbosity.

To perform a lookup on _[redhat.com](http://redhat.com:)_[](http://redhat.com:):

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/416_3.jpg)

Rerun the above with -v added. The output will be similar to that of the _dig_ command.

To perform a reverse lookup on the IP of _[redhat.com](http://redhat.com)_ using the -v flag to add details:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/417_1.jpg)

Refer to the command’s manual pages for options and more information.

**Performing Name Resolution with getent**

The _getent_ (_get entries_) command is a rudimentary tool that can fetch matching entries from the databases defined in the _nsswitch.conf_ file. This command reads the corresponding database and displays the information if found. For name resolution, use the _hosts_ database and _getent_ will attempt to resolve the specified hostname or IP address. For instance, run the following for forward and reverse lookups:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/418_1.jpg)

Check the command’s manual pages for available flags and additional information.
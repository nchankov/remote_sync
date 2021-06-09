# remote_sync

the script will continuously sync directory from local machine to remote server allowing 
you all changes which you make on the local machine to be distributed to the remote location.

Example:
Imagine you are working on a website project. You have dev environment configured on your
desktop machine. You need to go remote but you have only a slim laptop which
couldn't handle the whole dev environment.

So how you could solvethis?

With remote_sync you download your working files locally, so you can perform search, use some ide, changes are faser
On every change the rsync would be executed and you would update your remote work env, so you can test and work remotely

The script works as follows

1. sync remote to local location
2. loop and rsync the local to remote

if you are short on traffic, you could choose to have a local backup location which will check if there are differences
and if so then it would sync remotely. This will require double the space, but would limit the external traffic to the 
internet. That's useful if you are on mobile data or slow connection.

The other way is to use rsync constantly to loop and send the changes to the server. This way you don't need to have 
big storage, but network traffic would be bigger. Probably would be suitable if you are on wifi or with plan which
doesn't care for the traffic usage.

## Installation

1. clone or download the repository into your local env like so

```
git clone https://github.com/nchankov/remote_sync.git
```

2. make remote_sync/sync executable

```
chmod +x remote_sync/sync
```

3. modify the config file and specify the parameters

4. use the script by
```
remote_sync/sync -s
```

## Examples

This will use the default .config file from the remote_sync folder
```
remote_sync/sync -s
```

This will specify config file which would be used
```
remote_sync/sync -s -c /path/to/sync/config/file
```

## config file variables

### host

Remote host - usually this would be something like user@server.com

You need to create passwordless login between the local computer and the remote location otherwise it would ask you for password on
every rsync request

### remote_path

Remote path to the directory on the remote location. Something like /remote/location/path/ (make sure to add / at the end)

### local_path

Local location where the directory would be placed. Something like /local/location/path/ (make sure to add / at the end)

### local_path_check

If this variable is present, it would have backup location for the directory and rsync will be executed only if there are
differences between local_path and local_path_check
As I said - using this variable is useful if you are short on traffic
if that variable is commented , then rsync will be executed continuously but you won't need another directory

### auto

if present and set to "false" it would require manual
action on every sync interaction. This would be useful if you are on limited 
bandwith (mobile data). The option should be used instead of the local_path_check

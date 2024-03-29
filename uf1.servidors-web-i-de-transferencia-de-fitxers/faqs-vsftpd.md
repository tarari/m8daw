---
description: From https://github.com/richardcochran/vsftpd/blob/master/FAQ
---

# FAQS vsftpd

```
vsftpd frequently asked questions!!
-----------------------------------

Q) Can I restrict users to their home directories?
A) Yes. You are probably after the setting:
chroot_local_user=YES

Q) Why don't symlinks work with chroot_local_user=YES?
A) This is a consequence of how chroot() security works. As alternatives,
look into hard links, or if you have a modern Linux, see the powerful
"mount --bind".

Q) Does vsftpd support a limit on the number of users connected?
A1) Yes, indirectly. vsftpd is an inetd-based service. If use the popular
"xinetd" as your inetd, this supports per-service per-IP connection limits.
There is an example of this in the "EXAMPLE" directory.
A2) If you run vsftpd in "standalone" mode with the setting listen=YES, then
you can investigate the setting (e.g.):
max_clients=10

Q) Help! I'm getting the error message "refusing to run with writable anonymous
root".
A) vsftpd is protecting against dangerous configurations. The cause of this
message is usually dodgy ownership of the ftp home directory. The home
directory should NOT be owned by the ftp user itself. Neither should it
be writable by the ftp user. A way to fix this is:
chown root ~ftp; chmod -w ~ftp

Q) Help! I'm getting the error message "str_getpwnam".
A) The most likely cause of this is that the user that is configured as the
'nopriv_user' setting (often 'nobody') does not exist on your system. vsftpd
needs this user to run bits of itself with no privilege.

Q) Help! Local users cannot log in.
A) There are various possible problems.
A1) By default, vsftpd disables any logins other than anonymous logins. Put
local_enable=YES in your /etc/vsftpd.conf to allow local users to log in.
A2) vsftpd tries to link with PAM. (Run "ldd vsftpd" and look for libpam to
find out whether this has happened or not). If vsftpd links with PAM, then
you will need to have a PAM file installed for the vsftpd service. There is
a sample one for RedHat systems included in the "RedHat" directory - put it
under /etc/pam.d
A3) If vsftpd didn't link with PAM, then there are various possible issues. Is
the user's shell in /etc/shells? If you have shadowed passwords, does your
system have a "shadow.h" file in the include path?
A4) If you are not using PAM, then vsftpd will do its own check for a valid
user shell in /etc/shells. You may need to disable this if you use an invalid
shell to disable logins other than FTP logins. Put check_shell=NO in your
/etc/vsftpd.conf.

Q) Help! Uploads or other write commands give me "500 Unknown command.".
A) By default, write commands, including uploads and new directories, are
disabled. This is a security measure. To enable writes, put write_enable=YES
in your /etc/vsftpd.conf.

Q) Help! What are the security implications referred to in the
"chroot_local_user" option?
A) Firstly note that other ftp daemons have the same implications. It is a
generic problem.
The problem isn't too severe, but it is this: Some people have FTP user
accounts which are not trusted to have full shell access. If these
accounts can also upload files, there is a small risk. A bad user now has
control of the filesystem root, which is their home directory. The ftp
daemon might cause some config file to be read - e.g. /etc/some_file. With
chroot(), this file is now under the control of the user. vsftpd is
careful in this area. But, the system's libc might want to open locale
config files or other settings...

Q) Help! Uploaded files are appearing with permissions -rw-------.
A1) Depending on if this is an upload by a local user or an anonymous user,
use "local_umask" or "anon_umask" to change this. For example, use
"anon_umask=022" to give anonymously uploaded files permissions
-rw-r--r--. Note that the "0" before the "22" is important.
A2) Also see the vsftpd.conf.5 man page for the new "file_open_mode"
parameter.

Q) Help! How do I integrate with LDAP users and logins?
A) Use vsftpd's PAM integration to do this, and have PAM authenticate against
an LDAP repository.

Q) Help! Does vsftpd do virtual hosting setups?
A1) Yes. If you integrate vsftpd with xinetd, you can use xinetd to bind to
several different IP addresses. For each IP address, get xinetd to launch
vsftpd with a different config file. This way, you can get different behaviour
per virtual address.
A2) Alternatively, run as many copies as vsftpd as necessary, in standalone
mode. Use "listen_address=x.x.x.x" to set the virtual IP.

Q) Help! Does vsftpd support virtual users?
A) Yes, via PAM integration. Set "guest_enable=YES" in /etc/vsftpd.conf. This
has the effect of mapping every non-anonymous successful login to the local
username specified in "guest_username". Then, use PAM and (e.g.) its pam_userdb
module to provide authentication against an external (i.e. non-/etc/passwd)
repository of users.
Note - currently there is a restriction that with guest_enable enabled, local
users also get mapped to guest_username.
There is an example of virtual users setup in the "EXAMPLE" directory.

Q) Help! Does vsftpd support different settings for different users?
A) Yes - in a very powerful way. Look at the setting "user_config_dir" in the
manual page.

Q) Help! Can I restrict vsftpd data connections to a specific range of ports?
A) Yes. See the config settings "pasv_min_port" and "pasv_max_port".

Q) Help! I'm getting the message "OOPS: chdir".
A) If this is for an anonymous login, check that the home directory for the
user "ftp" is correct. If you are using the config setting "anon_root", check
that is correct too.

Q) Help! vsftpd is reporting times as GMT times and not local times!
A) This behaviour can be changed with the setting "use_localtime=YES".

Q) Help! Can I disable certain FTP commands?
A) Yes. There are some individual settings (e.g. dirlist_enable) or you can
specify a complete set of allowed commands with "cmds_allowed".

Q) Help! Can I change the port that vsftpd runs on?
A1) Yes. If you are running vsftpd in standalone mode, use the "listen_port"
directive in vsftpd.conf.
A2) Yes. If you are running vsftpd from an inetd or xinetd program, this
becomes an inetd or xinetd problem. You must change the inetd or xinetd
configuration files (perhaps /etc/inetd.conf or /etc/xinetd.d/vsftpd)

Q) Help! Will vsftpd authenticate against an LDAP server? What about a
MySQL server?
A) Yes. vsftpd uses PAM for authentication, so you need to configure PAM
to use pam_ldap or pam_mysql modules. This may involve installing the PAM
modules and then editing the PAM config file (perhaps /etc/pam.d/vsftpd).

Q) Help! Does vsftpd support per-IP limits?
A1) Yes. If you are running vsftpd standalone, there is a "max_per_ip"
setting.
A2) Yes. If you are running vsftpd via xinetd, there is an xinetd config
variable "per_source".

Q) Help! Does vsftpd support bandwidth limiting?
A) Yes. See vsftpd.conf.5 man page and investigate settings such as
"anon_max_rate" and "local_max_rate".

Q) Help! Does vsftpd support IP-based access control?
A1) Yes. vsftpd can integrate with tcp_wrappers (if built with this support).
It is enabled with the setting "tcp_wrappers=YES".
A2) Yes. vsftpd can be run from xinetd, which supports tcp_wrappers
integration.

Q) Help! Does vsftpd support IPv6?
A) Yes, as of version 1.2.0. Read the vsftpd.conf.5 man page.

Q) Help! vsftpd doesn't build, it fails with an error about being unable to
find -lcap.
A) Install the libcap package and retry the build. Seems to affect Debian
users a lot.
A) Install the libcap-devel. This certainly affects Fedora.

Q) Help! I've put settings in /etc/vsftpd.conf, but they are not taking
effect!
A) This is affecting some RedHat users - some RedHat versions put the config
file in /etc/vsftpd/vsftpd.conf.

Q) Help! vsftpd doesn't build, it complains about problems with incomplete
types in sysutil.c.
A) Your system probably doesn't have IPv6 support. Either use a more modern
system, use an older vsftpd (e.g. v1.1.3), or wait for a version of vsftpd
without this problem!

Q) Help! I'm getting messages along the lines of 500 OOPS: vsf_sysutil_bind
when trying to do downloads (particularly lots of small files).
A) vsftpd-1.2.1 should sort this out.

Q) Help! Does vsftpd support hiding or denying certain files?
A) Yes. Look at the hide_file and deny_file options in the manual page.

Q) Help! Does vsftpd support FXP?
A) Yes. An FTP server does not have to do anything special to support FXP.
However, you many get tripped up by vsftpd's security precautions on IP
addresses. In order to relax these precautions, have a look in the
vsftpd.conf.5 for pasv_promiscuous (and the less advisable port_promiscuous).

Q) Help! I'm getting the error "426 Failure writing network stream." on
downloads.
A) You shouldn't see this with v1.2.1 or newer versions of vsftpd. Older
versions of vsftpd can give this error if the user tries to download
something from an unusual filesystem (e.g. FAT), which don't support
performance features used by vsftpd. With vsftpd-1.1.3 and newer there is a
config workaround, use_sendfile=NO.

Q) Help! I'm using the pam_userdb login module and the login hangs.
A) This could be a bad interaction with glibc version 2.3 and PAM. A Debian
user reported this. The initial report is here:
http://lists.debian.org/debian-glibc/2003/debian-glibc-200309/msg00310.html

Q) Help! Does vsftpd support large files (>2Gb?).
A) Yes, it does.

Q) Help! Well, large file support doesn't seem to be working, then!
A1) Large file support first appeared in v1.1.0.
A2) Solaris large file support wasn't fixed until v1.2.2.
A3) FreeBSD large file support wasn't fixed until v1.2.2.
A4) The early Linux 2.6 kernels had a bug in this area - use v2.6.6 or newer.
A5) Are you sure your FTP _client_ correctly supports large files?

Q) Help! The built-in vsftpd listener is hanging or crashing!
A) A bug in this area is fixed in vsftpd v1.2.2. The problem has always existed
but seems to frequently trigger only on certain platforms. For example,
Fedora Core 1 - the suspected trigger is a glibc-2.3 platform, possibly in
combination with a NPTL-enabled kernel.

Q) Help! I'm using Solaris / Veritas and vsftpd is hanging!
A) Suspected bug with the Solaris / Veritas combination. With vsftpd-1.2.3
there is a possible workaround: no_log_lock=YES in your vsftpd.conf.5.

Q) Does vsftpd support SSL / TLS based encryption?
A) Yes, as of v2.0.0, this is supported for the control and data connections
(hurrah). You need a build of vsftpd with this support enabled, and then you
need to activate the ssl_enable setting. NOTE there are security considerations
with this support. Please make sure to read the ssl_enable section in the
vsftpd.conf.5 man page thoroughly before using.

Q) Help! I'm using FlashFXP and getting truncated files on download.
A) FlashFXP is buggy - particularly with SSL transfers. Upgrade to v3.0RC4
or newer, which is reported to be fixed.

Q) Help! I'm trying to build vsftpd, and I get an error along the lines of
"krb5.h: no such file or directory".
A) Yes, seems to be a problem with some RedHat setups. See
http://bugzilla.redhat.com/bugzilla/show_bug.cgi?id=111301 for details and
suggested workarounds.

Q) Help! I'm getting the error "OOPS: capset" when I try to connect to vsftpd.
A) This is an issue with SELinux enabled distributions. The solution is to
make sure the capability kernel module is loaded.

Q) Help! I'm getting the error "ftp: netin: Interrupted system call".
A) Seems to be a bug in ftp-tls, particularly with SSL transfers with
bandwidth limiting in effect.

Q) Help! When trying SSL transfers, users log in and are no longer restricted
to their home directory! They can browse the entire filesystem!
A) Most likely, your FTP client is in fact using the SSH protocol rather than
the FTP protocol - so sshd is in control and not vsftpd!
A) Of course, make sure you turn on the chroot_local_user option!!

Q) Help! I'm getting connections dropped whilst using gFTP for an SSL
connection.
A) The version of gFTP on my Fedora Core 10 installation appears to send the
"SIZE" command plain text during an SSL connection, which obviously breaks the
SSL connection.

Q) Help! SSL data connections are not working.
A) As of v2.1.0, vsftpd only accepts data connections that are reused sessions
of the control connection. This is a security measure. Unfortunately, not all
FTP clients reuse sessions (e.g. curl). You can disable this requirement by
changing require_ssl_reuse to NO.

Q) Blah.. blah..
A) For a good idea of what vsftpd can do, read the vsftpd.conf.5 man page
and the EXAMPLES.
```

\

---
layout: post
title: Some quick notes on compiling and running Samba 4 on SmartOS
---

# {{ page.title }}
<p class="meta">2013-04-19</p>

## Setup
 1. Follow [Jonathan Perkin's instructions for setting up a pkgsrc tree for builds](http://www.perkin.org.uk/posts/pkgsrc-on-smartos-zone-creation-and-basic-builds.html) (I used 2012Q4 on base64-1.9.1)
 1. Patch the wip/samba package:
<pre>
diff --git a/samba/PLIST b/samba/PLIST
index f69b907..1ae2141 100644
--- a/samba/PLIST
+++ b/samba/PLIST
@@ -187,7 +187,6 @@ lib/libndr.so.0
 lib/libndr.so.0.0.1
 lib/libnetapi.so
 lib/libnetapi.so.0
-lib/libnss_winbind.so
 lib/libnss_wins.so
 lib/libnss_wins.so.2
 lib/libpdb.so
@@ -753,7 +752,6 @@ lib/samba/service/winbind.so
 lib/samba/service/wrepl.so
 lib/samba/vfs/acl_tdb.so
 lib/samba/vfs/acl_xattr.so
-lib/samba/vfs/aio_fork.so
 lib/samba/vfs/aio_posix.so
 lib/samba/vfs/aio_pthread.so
 lib/samba/vfs/audit.so
</pre>

## Building and Running it
 1. Build and install samba
 1. Run the domain setup with an extra flag
<pre>
samba-tool domain provision --use-ntvfs --interactive
  (follow prompts)
cp /opt/local/etc/samba/private/krb5.conf /etc/krb5/krb5.conf
</pre>

## Next steps
 1. Create an SMF manifest (I haven't done this yet... I'm currently just running it manually for testing)
 1. (Also haven't done this yet: [Add the Global zone to the domain](http://wiki.smartos.org/display/DOC/Joining+SmartOS+to+an+Active+Directory+domain)

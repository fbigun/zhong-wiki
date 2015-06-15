aptftp.conf

```
APT::FTPArchive::Release {
Origin "Debian";
Label "Debian";
Suite "stable";
Codename "lenny";
Architectures "amd64";
Components "main";
Description "Rocky Debian Archive";
};
```

aptgenerate.conf

```
Dir::ArchiveDir ".";
Dir::CacheDir ".";
TreeDefault::Directory "pool/";
TreeDefault::SrcDirectory "pool/";
Default::Packages::Extensions ".deb";
Default::Packages::Compress ". gzip bzip2";
Default::Sources::Compress "gzip bzip2";
Default::Contents::Compress "gzip bzip2";

BinDirectory "dists/lenny/main/binary-mipsel" {
Packages "dists/lenny/main/binary-mipsel/Packages";
Contents "dists/lenny/Contents-mipsel";
SrcPackages "dists/lenny/main/source/Sources";
};

Tree "dists/lenny" {
Sections "main";
Architectures "mipsel source";
};
```

```
cd /var/www/loongson2f
apt-ftparchive generate -c=aptftp.conf aptgenerate.conf
apt-ftparchive release -c=aptftp.conf dists/lenny > dists/lenny/Release
rm -f dists/lenny/Release.gpg
gpg -u 5012729B  -bao dists/lenny/Release.gpg dists/lenny/Release
```
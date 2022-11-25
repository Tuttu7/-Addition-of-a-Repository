#### If we need to install a package which is not listed in the offical respositories we would need to add a new repository. Adding a repository in YUM is a manual operation, which consists in creating a file with the .repo extension under the folder /etc/yum.repos.d.The file must contain all the information about the custom repository that we are connecting to.

```
/etc/yum.repos.d/new.repo
name=
baseurl=
enabled=
gpgcheck=
```

 

#### In APT, though, things are quite different. The GPG key of the repository must be downloaded and added to the APT keyring with apt-key add :

```
wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | sudo apt-key add -
```

#### Then, at this point, the repository can be added through add-apt-repository –yes followed by the URL :

```
add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/
```

#### Contrary to YUM, all the repositories are saved in a single file, /etc/apt/sources.list.


#### Removal of repository. Removing a repository in YUM is performed differently depending on how it’s been installed.We can run the following command and analyze its output:

```

rpm -qa | grep -i CUSTOM_REPOSITORY
```


#### If the repository’s RPM package is found, it means it’s been installed through RPM, and we can remove it using -e :

```
rpm -e CUSTOM_REPOSITORY_RPM_PACKAGE
```

#### Otherwise, we can simply delete the repository file :

```
rm /etc/yum.repos.d/CUSTOM_REPOSITORY.repo
```


#### We can also disable it without deleting it, by simply turning enabled=1 to enabled=0 in the repository file. In APT, on the other hand, we can simply do:


```
add-apt-repository --remove ppa:CUSTOM_REPOSITORY/ppa
```

#### Alternatively, we can comment out the rows relative to the repository in the /etc/apt/sources.list file.

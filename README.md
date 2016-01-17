# FreeRTOS
http://www.freertos.org/

## Overview
This repository is an unofficial mirror of [FreeRTOS](http://www.freertos.org/). You can find the latest [official FreeRTOS on SourceForge](http://sourceforge.net/projects/freertos). [Pax Instruments](http://paxinstruments.com/) is not associated with FreeRTOS or the maintainer [Real Time Engineers ltd.](http://www.freertos.org/RTOS-contact-and-support.html), we just like them a lot :-)

The only change made in this Github repository is the addition of this README.md file. For information directly from the FreeRTOS team, read [readme.txt](https://github.com/PaxInstruments/freertos/blob/master/readme.txt).

## Obtaining FreeRTOS via Github
You can directly download the latest version of this repository: [Download now](https://github.com/istarc/freertos/archive/master.zip)

To clone the entire git repository use

`git clone https://github.com/istarc/freertos.git`

You will probably want to check out a specific version of FreeRTOS rather than using the current development version. To see the list of releases use

`git tag V8.2.3`

To checkout a release type
git checkout V8.2.3

## Updating FreeRTOS via Github
Ensure you checkout the master branch and are not on a tag.

`git checkout master`

Then you can update from the Github repository.

`git pull`

## Repository update notes
The information in this section is for the maintainer of this Github repository. You will probably not need to knwo this. This Github repository was created using the follow method.

1. Clone the original svn repository

git svn clone -s svn://svn.code.sf.net/p/freertos/code/ -T trunk -b branches -t tags

2. Create tags
```
git for-each-ref --format="%(refname:short) %(objectname)" refs/remotes/origin/tags | 
cut -d / -f 3- | 
while read tag ref ; 
  do msg=$(git log --pretty=format:'%s' -1 ${ref}) ; 
  git tag -f -a $tag -m "$msg" ${ref}^ ; 
done
```

3. Keep repository updated

```
git checkout master
git pull
git svn rebase
git push
git rebase --abort
# Update any tags
git for-each-ref --format="%(refname:short) %(objectname)" refs/remotes/origin/tags | 
cut -d / -f 3- | 
while read tag ref ; 
  do msg=$(git log --pretty=format:'%s' -1 ${ref}) ; 
  git tag -f -a $tag -m "$msg" ${ref}^ ; 
done
git push origin --tags
```

<h1 align="center">TUXI-UnGoogled [Unmaintained]</h1>
<p align="center">A CLI tool that scrapes Whoogle search results and SERPs that provides instant and concise answers</p>

```
This is currently in beta as whoogle search's
result page does not use id's therefore we
have to use CSS paths. Which are non-unique, 
so its difficult to parse the results.
However it's still better than using google's trackers.
```

##  

![Examples](https://github.com/spector-9/tuxi/blob/main/gif/demo.gif)

### How does this work?

The script uses `pup` to scrape Whoogle search results and SERPs.
If the query returns several results, Tuxi will choose the most 
relevant result on the basis of priority.

In addition to scraping, `tuxi` also uses `jq`, `awk` and `sed` 
to process and return results, and `recode` to unescape html.


[Watch this video for more info](https://youtu.be/EtwWvMa8muU)
> Also checkout BugsWriter's YouTube channel for more scripts like this.

## Requirements

* [pup](https://github.com/ericchiang/pup) - CLI tool for processing HTML.
* [recode](https://github.com/rrthomas/recode) - Charset converter tool and library.
* [jq](https://github.com/stedolan/jq) - Command-line JSON processor.



## Installation


### Make
```sh
$ git clone https://github.com/spector-9/tuxi.git && cd tuxi/
$ sudo make install
```
> To update, just `git pull` on your local tuxi repository and reinstall with `sudo make install`.  
> To uninstall, simply run `sudo make uninstall`.

## After Installation

Whoogle search is a deployable search engine. 
Meaning you can deploy your own search engine environment or you can use the public instances listed on whoogle's git.

### Easy Method
* Find a Public Instance from [Whoogle's git](https://github.com/benbusby/whoogle-search#public-instances).
* Replace the url with -u flag. Eg.
```
tuxi -u url_here
```

![Adding URL](https://github.com/spector-9/tuxi/blob/main/gif/url.gif)

no need to add https or www in the beginning.

### Recommended Method
**This is by no means difficult but it requires a little time to setup.**
* Create an account on [Heroku](https://www.heroku.com/).
* Deploy the search engine by following the instructions [here](https://github.com/benbusby/whoogle-search#install)
* After deployment change the url using -u flag as described above.
* You can deploy it anywhere if you don't want to use heroku.

*Heroku apps become inactive after sometime which takes some time to reload so you can use cronjobs to setup automated pings*
If you know how to use cronjobs then just add the following job
```
*/20 7-23 * * * /bin/curl -s https://<your heroku app name>.herokuapp.com > /dev/null
```

If you don't then
* Install a cronjob manager like 'cronie'
* run following commands
```
sudo systemctl enable --now cronie
crontab -e
```
Now paste the line above & save.


## Usage

```sh
$ tuxi "Is Linux better than Windows?"
---
Linux has a reputation for being fast and smooth while
Windows 10 is known to become slow and slow over
time. Linux runs faster than Windows 8.1 and Windows 10
along with a modern desktop environment and qualities of the
operating system while windows are slow on older hardware.
---
```
* Quotations are optional, but should be used if you want to search with special characters (?=!|&<>%$#/\\).
* You can also write your query as a statement, e.g: `tuxi linus torvalds birthday`.
* The -r option will make the output not have formatting, which can be convenient for use in scripts.
* The -q option silences "Did you mean?" and Tuxi's greeting on calling `tuxi`.

Use `-h` to display the help message.

```sh
$ tuxi -h
Usage: tuxi [options] query

Options:
  -h                    Show this help message and exit.
  -r                    Raw search results.
                        (no pretty output, no colors)
  -q                    Only output search results.
                        (silences "Did you mean?", greeting, usage)
  -u                    Change the current URL
                        (change the URL for Whoogle's instance)
```

## Features

**Gives corrections**
```sh
$ tuxi linux torvalds birthday
> Did you mean linus?
---
28 December 1969
---
```

**When you know it's actually linux torvalds** <kbd>-q option</kbd>
```sh
$ tuxi -q linux torvalds birthday
---
28 December 1969
---
```

**Raw formatting for output (no colors)** <kbd>-r option</kbd>
> Useful for e.g scripting `notify-send`.
```sh
$ tuxi -r linux torvalds birthday
> Did you mean linus?
28 December 1969
```

**Math operations**
```sh
$ tuxi "log(30)"
---
1.4771212547196624
---
```

**Translate**
```sh
$ tuxi "I love you in japanese"
---
わたしは、あなたを愛しています
---
$ tuxi "わたしは、あなたを愛しています in english"
---
I love you
---
```

**And much more (lyrics, weather, conversions...)**

## License

This project is licensed under [GPL-3.0](./LICENSE).

## Contributing

If you want to contribute, please see [CONTRIBUTING](./.github/ISSUE_TEMPLATE/CONTRIBUTING.md).


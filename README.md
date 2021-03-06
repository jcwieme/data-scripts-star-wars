# Scripts from Star Wars movies

## Table Of Contents

- [Scripts from Star Wars movies](#scripts-from-star-wars-movies)
  - [Table Of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Why this repo](#why-this-repo)
  - [Progression in the project](#progression-in-the-project)
  - [What can you find here](#what-can-you-find-here)
  - [Some code](#some-code)
  - [Credits](#credits)

## Overview

All the complete scripts of the first 6 **Star Wars** movies, as well as a light version of each containing only the dialogues and the places where they took place.

Likewise, you will find the **images** of each of the **characters** who had an interaction in the films.

In the folder ***data*** , are the CSV files of each film with information on the dialogues such as: the **number of words** per interaction, the **types of words**, the **duration** of the **interaction**, **who** speaks to **whom** and the **location**.

If you like the work then do not hesitate to visit my [site](https://www.jeanchristophewieme.be/).

## Why this repo

This project was initially a **personal project** but with the work accomplished, I find it important to share with the community.

The idea for the **Star Wars** project came to me after a conference on data visualization at the **[KIKK festival](http://kikk.be/)** in Namur in **Belgium**. The speaker (**[Nadieh Bremer](https://www.visualcinnamon.com/)**) made me want to create a **data-visualization** and what could be better than the theme of Star Wars. My **data-visualization** will be visible later.

At first, I recovered the scripts of the first 6 films. I laid them out in markdown files in order to keep only the **dialogues**, the **speakers** and the **places**. I accompanied the script files with one file per film each time containing all the characters.

In the continuity of my work, I encoded the markdown files in HTML so that I could automatically **extract** the data I wanted with **Javascript**. At the same time, I created a small **script** that counted the words.

The second part of my work consisted of watching all the films and checking that everything was correct in terms of scripts.

This done, I encoded each film in a **numbers file** with several data including among others : the **speaker**, the **interlocutor**, the **content**, the **duration**, the **place**, the **number of words**, the **type of words**, etc. Thanks to the subtitle files, I was able to recover the duration of the talks and check all the data a second time.

## Progression in the project

A small overview of the progress of the project.

- [x] ~~Recover script files~~ (3th January 2020)
- [x] ~~Transcription and cleaning in markdown~~ (8th January 2020)
- [x] ~~Adding data in the sheet~~ (8th January 2020)
- [ ] Adding listeners
- [ ] Adding durations
- [ ] Adding sorts of words
- [ ] Creating CSV files for each movie
- [ ] Creating JSON files for each movie

## What can you find here

In this repo, you can find several files about the Star Wars univers.

| Folder      | Description |
| ----------- | ----------- |
| :open_file_folder: [Sources](https://github.com/jcwieme/data-scripts-star-wars/tree/master/1.%20Sources) | All source files that were used to collect the data |
| :open_file_folder: [Markdown](https://github.com/jcwieme/data-scripts-star-wars/tree/master/2.%20Markdown) | Markdown files with dialogs, speakers and location |
| :open_file_folder: [JSON for sheet](https://github.com/jcwieme/data-scripts-star-wars/tree/master/3.%20JSON%20for%20sheet) | JSON files format to populate the Sheet file |
| :open_file_folder: [Data sheet](https://github.com/jcwieme/data-scripts-star-wars/tree/master/4.%20Data%20sheet) | Sheet file which gathers all the information for each film |
| :open_file_folder: [Data CSV](https://github.com/jcwieme/data-scripts-star-wars/tree/master/5.%20Data%20CSV) | CSV file ready to use for each film |

## Some code

> My count words function used for the project :

```javascript
function countWords(s){
    s = s.replace(/(^\s*)|(\s*$)/gi,"")
    s = s.replace(/[ ]{2,}/gi," ")
    s = s.replace(/[...]/gi," ")
    s = s.replace(/[(]+.+[)]/gi," ")
    s = s.replace(/\n /,"\n")
    return s.split(' ').filter(function(str){return str!="";}).length
}
```

> Code to make the json

```javascript
const uls = document.querySelectorAll('ul')
var global = []
var wordsGlobal = []
let where = null

let timePerWords = Math.round(83672 / 9595);

uls.forEach(ul => {
    let previousEl = ul.previousElementSibling
    let lis = [...ul.getElementsByTagName('li')]

    if (previousEl !== null) {
        if (previousEl.nodeName === "P") {
            where = previousEl.innerText
        }
    }

    lis.forEach(li => {
        let content = li.innerText.split(" : ")
        let number = 0
        let text = content[1]
        let textFormat = null
        let peoples = content[0].split(' to ')

        if (typeof text !== 'undefined') {
            textFormat = formatSentence(text)
            number = countWords(textFormat)
        }

        global.push({
            "from": peoples[0],
            "to": peoples[1],
            "text": text,
            "where": where,
            "number": number,
            "time": number * timePerWords
        })
    })
})

let data = JSON.stringify(global)
```

> My PHP file to get the total speech time on screen based on the SRT

```php
  $data = file_get_contents('./srt.txt', false);
  $res = preg_replace("/\*([0-9])\*/", "", $data);
  $res2 = preg_replace("/[^0-9:,>]/", " ", $res);
  $res3 = preg_replace('!\s+!', ' ', $res2);
  $res4 = preg_replace('/ , /', ' ', $res3);
  $res5 = preg_replace('/ > /', '>', $res4);
  $res6 = preg_replace('!\s+!', ' ', $res5);
  $res7 = explode(" ", $res6);

  $minutesGlobal = 0;
  $msGlobal = 0;

  foreach($res7 as $part) {
    $explode = explode('>', $part);

    if (sizeof($explode) == 2) {

      $explode[0] = preg_replace("/,/", ":", $explode[0]);
      $explodeNumbers = explode(':',$explode[0]);
      $explode[1] = preg_replace("/,/", ":", $explode[1]);
      $explodeNumbers2 = explode(':',$explode[1]);

      $ms = (int)$explodeNumbers2[3] - (int)$explodeNumbers[3];
      $secondes = (int)$explodeNumbers2[2] - (int)$explodeNumbers[2];
      $minutes = (int)$explodeNumbers2[1] - (int)$explodeNumbers[1];
      $hours = (int)$explodeNumbers2[0] - (int)$explodeNumbers[0];

      $minutesGlobal += $minutes;
      $msGlobal += $ms;
    }
  }

  echo $minutesGlobal . ' ' . $msGlobal;
```

## Credits

> The storyline, characters and images represented in this repo belong to the respective owners

| Links      | Description |
| ----------- | ----------- |
| [DISNEY](https://www.disney.com/) | All content belong to Disney |
| [IMSDB](https://www.imsdb.com/) | Scripts from movies |
| [YIFY](https://yts-subs.com/) | Subtitles files |
| [MARKDOWN TO HTML](https://markdowntohtml.com/) | Convert markdown to html |
| [JSON PARSER](http://json.parser.online.fr/) | Parser the JSON |
| [CSV-JSON](https://www.csvjson.com/json2csv) | Convert JSON to CSV |
| [WORDCOUNTER](https://wordcounter.net/) | Count word if needed |
| [REGEXR](https://regexr.com/) | For Regular Expressions |
| [WORDPOS](https://www.npmjs.com/package/wordpos-web) | Part-of-speech for type of words  |

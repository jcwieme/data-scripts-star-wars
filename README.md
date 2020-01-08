# Scripts from Star Wars movies

All the complete scripts of the first 6 **Star Wars** movies, as well as a light version of each containing only the dialogues and the places where they took place.

Likewise, you will find the **images** of each of the **characters** who had an interaction in the films.

In the folder ***data*** , are the CSV files of each film with information on the dialogues such as: the **number of words** per interaction, the **types of words**, the **duration** of the **interaction**, **who** speaks to **whom** and the **location**.

## Why this repo

This project was initially a **personal project** but with the work accomplished, I find it important to share with the community.

The idea for the **Star Wars** project came to me after a conference on data visualization at the **[KIKK festival](http://kikk.be/)** in Namur in **Belgium**. The speaker (**[Nadieh Bremer](https://www.visualcinnamon.com/)**) made me want to create a **data-visualization** and what could be better than the theme of Star Wars. My **data-visualization** will be visible later.

At first, I recover the scripts of the first 6 films.
I laid them out in markdown files in order to keep only the **dialogues**, the **speakers** and the **places**. I accompanied the script files with one file per film each time containing all the characters.

The second part of my work consisted of watching all the films and checking that everything was correct in terms of scripts.

This done, I encoded each film in a **numbers file** with several data including among others : the **speaker**, the **interlocutor**, the **content**, the **duration**, the **place**, the **number of words**, the **type of words**, etc. Thanks to the subtitle files, I was able to recover the duration of the talks and check all the data a second time.

## What can you find here

In this repo, you can find several files about the Star Wars univers.

## Credits

* [IMSDB](https://www.imsdb.com/) : scipts from movies
* [YIFY](https://yts-subs.com/) : subtitles files
* [MarkdownToHtml](https://markdowntohtml.com/) : convert markdown to html
* [JSON Parser](http://json.parser.online.fr/) : Parese the JSON
* [CSV-JSON](https://www.csvjson.com/json2csv) : Convert JSON to CSV
* [WORDCOUNTER](https://wordcounter.net/) : Count word if needed

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

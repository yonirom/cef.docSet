CEF Docset for Dash
===================

Usage Instructions:
-------------------

* Clone repository
* Add local directory to dash docsets via Dash settings

Creation Instructions:
----------------------

* get http://www.magpcss.net/cef_downloads/index.php?file=cef_binary_3.1750.1738_docs.7z
* create directory stucture: cef.docSet/Contents/Resources/Documents
* Unzip documenetation into created dir
* from cef.docSet/Contents/Resources/Documents/projects/(default) run:
```
echo 'CREATE TABLE searchIndex(id INTEGER PRIMARY KEY, name TEXT, type TEXT, path TEXT);' | sqlite3 ../../../docSet.dsidx
echo 'CREATE UNIQUE INDEX anchor ON searchIndex (name, type, path);' | sqlite3 ../../../docSet.dsidx
grep ^\<H3 * | sed -e 's/\(.*html\):<H3>\(.*\)<\/H3>/INSERT OR IGNORE INTO searchIndex(name, type, path) VALUES ("\2", "Method", "projects\/(default)\/\1#\2");/' | sqllite3 ../../../docSet.dsidx
grep ^Class * | sed -e 's/\(.*html\):Class  \(.*\)<\/H2>/INSERT OR IGNORE INTO searchIndex(name, type, path) VALUES ("\2", "Class", "projects\/(default)\/\1");/' | sqllite3 ../../../docSet.dsidx
```
* Place icon in docSet root

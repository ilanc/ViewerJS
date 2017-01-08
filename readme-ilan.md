# Customisations to ViewerJS

## Goal

Make it possible to load a pdf locally (from file-open dialog) without requiring upload/download.

## Solution
see index.loadLocalPdf.html

## Notes

Build process is a bit of a bugger. Built in ubuntu on windows-10 (IRONWILL). Required:
1. nodejs
2. npm
3. cmake
4. make
5. java jre

```
sudo apt-get update
sudo apt-get install cmake nodejs npm default-jre
```

## Prototype

see C:\dev\build\viewerjs-0.5.9\ViewerJS

* index.html = added `<input type="file">` at the top so we have a file-open dialog
* PDFViewerPlugin2.js = unnecessary = just need to convert 'location' from arrayBuf to Uint8Array, and can do this externally
* viewer2.js = required = prevent initializeAboutInformation from creating multiple ViewerJS buttons
* app.js = need to move LoadLocalPdf to an API which can be called from parent of iframe

## How to build (from scratch)

run ubuntu / git bash
```
cd /c/dev
mkdir build
cd build
cmake ../ViewerJS
make
```

## How to rebuild

run ubuntu / git bash
```
cd /c/dev/build
rm index.html *.js
make

kill %1   # if live-server is running
mv viewerjs-0.5.9/ viewerjs-0.5.9-old
make
cp viewerjs-0.5.9-old/ViewerJS/ilan.html viewerjs-0.5.9/ViewerJS/
```
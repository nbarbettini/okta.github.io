# Hugo version of okta blog
## TODO:

- Create basic project layout
- Migrate layouts to hugo theme
- Porting the blog over (/blog)
- Porting the RSS feeds over (see all the .xml files in the _source directory?
Those RSS feeds need to be duplicated in the exact same format as they are
used for automation)
- Port over the documentation (this should be easy). We host our developer
documentation in this project as well currently. Eventually we'll extract it
out into a separate project, but for now we should port it over as is.
This will involve migrating all the /documentation content.

## How to build prod version
```bash
brew install hugo
hugo
```

## Detailed TODO:
### Transform static files progress:
- [x] assets
- [x] css
- [x] js
- [x] img

### Transform layouts progress:
- [x] baseof.html
- [x] head.html
- [x] header.html
- [x] footer.html
- [x] post-footer.html


### Port over the documentation 
- [x] We host our developer documentation in this project as well currently. 
- [x] migrating all the /documentation content.

## How to migrate tags:
```bash
python scripts/hugo_import_jekyll.py --target=_source/_posts --output=hugo/content/blog
for dir_name in $(ls -d1 _source/_docs/*/)
do
    code_path=`basename ${dir_name}`
    python scripts/hugo_import_jekyll.py --target=_source/_docs/${code_path} --output=hugo/content/docs/${code_path}
done

for dir_name in $(ls -d1 _source/_code/*/)
do
    code_path=`basename ${dir_name}`
    python scripts/hugo_import_jekyll.py --target=_source/_code/${code_path} --output=hugo/content/code/${code_path}
done

python scripts/hugo_import_jekyll.py --target=_source/_change-log --output=hugo/content/docs/change-log
# Usually you have alias=cp='cp -i'
/bin/cp -rf  _source/_assets/img/* hugo/themes/okta/static/img
/bin/cp -rf  _source/_assets/js/* hugo/themes/okta/static/js
cd _source/_assets/css/
scss okta.scss okta.css
scss page-search.scss page-search.css
cd ../../../
/bin/cp -rf _source/_assets/css/*.css hugo/themes/okta/static/css/
/bin/cp -rf _source/_assets/fonts/* hugo/themes/okta/static/fonts
/bin/cp -rf _source/_data/* hugo/data/
```
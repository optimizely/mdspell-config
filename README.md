# instructions

to be used along with `git@github.com:juancarlostong/node-markdown-spellcheck.git` in this branch: `jctong/generate_spelling_file`

```
for i in `ls |grep -- '-sdk$'`;do pushd $i; git checkout master; git pull; ln -s ~/gh/mdspell-config/.spelling; /Users/jtong/gh/node-markdown-spellcheck/bin/mdspell -a -n -r --en-us '**/*.md' 2>&1 >/dev/null | grep -v ^$ | sort | uniq > ~/gh/mdspell-config/$(basename $PWD); rm .spelling; popd; done

cat *-sdk | sort | uniq >> .spelling
```


inspect contents of .spelling and remove actual typos

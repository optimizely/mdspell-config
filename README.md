# instructions

to be used along with `git@github.com:juancarlostong/node-markdown-spellcheck.git` in this branch: `jctong/generate_spelling_file`

```
for i in `ls |grep -- '-sdk$'`;do pushd $i; git checkout master; git pull; ln -s ~/gh/mdspell-config/.spelling; /Users/jtong/gh/node-markdown-spellcheck/bin/mdspell -a -n -r --en-us '**/*.md' 2>&1 >/dev/null | grep -v ^$ | sort | uniq > ~/gh/mdspell-config/$(basename $PWD); rm .spelling; popd; done

# merge newly generated file with existing .spelling dictionary
cat <file-generated-in-prev-step> .spelling | sort | uniq > a

# compare line number difference between the existing .spelling and the "a" (the new .spelling)
wc -l a .spelling

# look at the differences
diff a .spelling

# make the new additions official
mv a .spelling

git add . && git commit && git push
```


inspect contents of .spelling and remove actual typos


notes for manually running:

```
ln -s ~/gh/mdspell-config/.spelling
/Users/jtong/gh/node-markdown-spellcheck/bin/mdspell -a -n -r --en-us '**/*.md' 2>&1 >/dev/null | grep -v ^$ | sort | uniq > ~/gh/mdspell-config/$(basename $PWD)
rm .spelling

# babelfish_distribution
Test Babelfish zip distribution


```sh
export EXTTAG=BABEL_1_0_0
export EXTREPO=babelfish_extensions
export ENGREPO=postgresql_modified_for_babelfish
export ENGTAG=BABEL_1_0_0__PG_13_4
export EXTDIR=${EXTREPO}-${EXTTAG}
export ENGDIR=${ENGREPO}-${ENGTAG}

cd test
curl -L https://github.com/babelfish-for-postgresql/babelfish_extensions/archive/refs/tags/BABEL_1_0_0.zip --output BABEL_1_0_0.zip
curl -L https://github.com/babelfish-for-postgresql/postgresql_modified_for_babelfish/archive/refs/tags/BABEL_1_0_0__PG_13_4.zip --output BABEL_1_0_0__PG_13_4.zip

unzip BABEL_1_0_0__PG_13_4.zip
unzip BABEL_1_0_0.zip

mv ${EXTDIR}/contrib/* ${EXTDIR}/

# [[ -d  ${EXTDIR}/contrib && ! -s ${EXTDIR}/contrib ]] && rm -fr ${EXTDIR}/contrib 
rm -fr ${EXTDIR}/contrib 
mv ${EXTDIR}/** ${ENGDIR}/contrib

# Extract the Release Notes from the website
curl https://raw.githubusercontent.com/babelfish-for-postgresql/babelfish_project_website/a9bbeb3aeb2305914ae802806df21d7b7fbd1ec9/_releases/release_notes_1.0.0.md | sed '/---/,/---/d' > ${ENGDIR}/RELEASE_NOTES.md
```

(
    cd postgresql_modified_for_babelfish-BABEL_1_0_0__PG_13_4 ;
    zip -r ../BABEL_1_0_0__PG_13_4.zip * ;
    tar cfz ../BABEL_1_0_0__PG_13_4.tar.gz ** 
)

drwxrwxr-x 5 tresma tresma 4.0K Dec 15 08:14 babelfish_extensions-BABEL_1_0_0
drwxrwxr-x 7 tresma tresma 4.0K Nov  4 17:42 postgresql_modified_for_babelfish-BABEL_1_0_0__PG_13_4



git archive --format=tar \
    --remote=git@github.com:babelfish-for-postgresql/postgresql_modified_for_babelfish.git \
    main  | tar -xf -

```
git remote add engine git@github.com:babelfish-for-postgresql/postgresql_modified_for_babelfish.git
git remote add extensions git@github.com:babelfish-for-postgresql/babelfish_extensions.git
git checkout tag file 
```

```
cd ..
export EXTTAG=${{ matrix.babel }}
export ENGTAG=${{ matrix.engine }}
export EXTREPO=babelfish_extensions
export ENGREPO=postgresql_modified_for_babelfish
export EXTDIR=${EXTREPO}-${EXTTAG}
export ENGDIR=${ENGREPO}-${ENGTAG}

curl -L https://github.com/babelfish-for-postgresql/${EXTREPO}/archive/refs/tags/${EXTTAG}.zip --output ${EXTTAG}.zip
curl -L https://github.com/babelfish-for-postgresql/${ENGREPO}/archive/refs/tags/${ENGTAG}.zip --output ${ENGTAG}.zip

unzip ${ENGTAG}.zip
unzip ${EXTTAG}.zip

mv ${EXTDIR}/contrib/* ${EXTDIR}/

# [[ -d  ${EXTDIR}/contrib && ! -s ${EXTDIR}/contrib ]] && rm -fr ${EXTDIR}/contrib 
rm -fr ${EXTDIR}/contrib 
mv ${EXTDIR}/** ${ENGDIR}/contrib

# Extract the Release Notes from the website
curl https://raw.githubusercontent.com/babelfish-for-postgresql/babelfish_project_website/a9bbeb3aeb2305914ae802806df21d7b7fbd1ec9/_releases/release_notes_1.0.0.md | sed '/---/,/---/d' > ${ENGDIR}/RELEASE_NOTES.md
```


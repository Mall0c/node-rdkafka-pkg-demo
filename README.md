This demo's purpose is to show that [pkg](https://www.npmjs.com/package/pkg) unfortunately has problems with symlinks in node_modules. 
While this might occur rarely, Blizzard's [node-rdkafka library](https://github.com/Blizzard/node-rdkafka/) has four symlinks in their package:

```
richards@richards<path-to-project>:$ ls -lR node_modules/ | grep ^l
lrwxrwxrwx 1 richards richards       17 Mär 16 15:03 librdkafka++.so -> librdkafka++.so.1
lrwxrwxrwx 1 richards richards       15 Mär 16 15:03 librdkafka.so -> librdkafka.so.1
lrwxrwxrwx 1 richards richards       15 Mär 16 15:03 librdkafka.so -> librdkafka.so.1
lrwxrwxrwx 1 richards richards      17 Mär 16 15:03 librdkafka++.so -> librdkafka++.so.1
```

Their location is:

* node_modules/node-rdkafka/build/deps/librdkafka++.so
* node_modules/node-rdkafka/build/deps/librdkafka.so
* node_modules/node-rdkafka/deps/librdkafka/src/librdkafka.so
* node_modules/node-rdkafka/deps/librdkafka/src-cpp/librdkafka++.so

Once you try to build a binary by issuing ```npm run package```, you'll see in the terminal that the build freezes at the symlink. This leaves the project unable to be packaged with pkg.

Steps to reproduce:

* npm install
* npm run package
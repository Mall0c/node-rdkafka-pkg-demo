This demo's purpose is to show that [pkg](https://www.npmjs.com/package/pkg) unfortunately has problems with symlinks in node_modules. 
While this might occur rarely, the node-rdkafka library has four symlinks in their package:

```
richards@richards:$ ls -lR node_modules/ | grep ^l
lrwxrwxrwx 1 richards richards       17 Mär 16 15:03 librdkafka++.so -> librdkafka++.so.1
lrwxrwxrwx 1 richards richards       15 Mär 16 15:03 librdkafka.so -> librdkafka.so.1
lrwxrwxrwx 1 richards richards       15 Mär 16 15:03 librdkafka.so -> librdkafka.so.1
lrwxrwxrwx 1 richards richards      17 Mär 16 15:03 librdkafka++.so -> librdkafka++.so.1
```

Once you try to build a binary by issuing ```npm run package```, you'll see in the terminal that the build freezes at the symlink. This leaves the project unable to be packaged with pkg.

Steps to reproduce:

* npm install
* npm run package
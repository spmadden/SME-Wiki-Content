#### Writing a finalize() Method

Before an object is garbage collected, the runtime system calls its finalize() method. The intent is for finalize() to release system resources such as open files or open sockets before getting collected.

Your class can provide for its finalization simply by defining and implementing a method in your class named finalize(). Your finalize() method must be declared as follows:

``` java
        protected void finalize () throws throwable
```

This class opens a file when its constructed:

``` java
        class OpenAFile {
            FileInputStream aFile = null;
            OpenAFile(String filename) {
                try {
                    aFile = new FileInputStream(filename);
                } catch (java.io.FileNotFoundException e) {
                    System.err.println("Could not open file " + filename);
                }
            }
        }
```

To be well-behaved, the OpenAFile class should close the file when its finalized. Here's the finalize() method for the OpenAFile class:

``` java
        protected void finalize () throws throwable {
            if (aFile != null) {
                aFile.close();
                aFile = null;
            }
        }
```

If your class's superclass has a finalize() method, then your class's finalize() method should probably call the superclass's finalize() method after it has performed any of its clean up duties. This cleans up any resources the object may have unknowingly obtained through methods inherited from the superclass.

``` java
        protected void finalize() throws Throwable {
            . . .
            // clean up code for this class here
            . . .
            super.finalize();
        }

```

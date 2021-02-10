# yamlthing
just a random thing that reads some random yaml in a strict way

this illustrates that YAML is not too terrible, given some data model checking behind:

```

ayourtch@ayourtch-lnx:~/rust/yamlthing$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/yamlthing`
thread 'main' panicked at 'called `Result::unwrap()` on an `Err` value: Message("invalid type: map, expected a string", Some(Pos { marker: Marker { index: 21, line: 2, col: 13 }, path: ".[0].name" }))', src/main.rs:24:60
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
ayourtch@ayourtch-lnx:~/rust/yamlthing$ git diff
diff --git a/foo.yaml b/foo.yaml
index a0147ef..1e6286b 100644
--- a/foo.yaml
+++ b/foo.yaml
@@ -1,8 +1,8 @@
 - name:
-  valueFrom:
-    secretKeyRef:
-       name: foo
-       key: bar 
+    valueFrom:
+      secretKeyRef:
+         name: foo
+         key: bar 
 - name:
   valueFrom:
     secretKeyRef:
ayourtch@ayourtch-lnx:~/rust/yamlthing$ git checkout .
ayourtch@ayourtch-lnx:~/rust/yamlthing$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/yamlthing`
Hello, here's your yaml: [
    Thingy {
        name: "~",
        valueFrom: secretKeyRef(
            KeyRef {
                name: "foo",
                key: "bar",
            },
        ),
    },
    Thingy {
        name: "~",
        valueFrom: secretKeyRef(
            KeyRef {
                name: "foo",
                key: "bar",
            },
        ),
    },
]
ayourtch@ayourtch-lnx:~/rust/yamlthing$ 
```

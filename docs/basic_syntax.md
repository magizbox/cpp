# C/C++

## Hello World

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "hello world";
}
```

## Convention

### Naming

```
variable_name_like_this
class_data_memeber_name_like_this_
kConstantNamesLikeThis
ClassNameLikeThis
filenamelikethis_myusefulclass_test.cc
```

### Comment

#### Class Comment

```cpp
// Iterates over the contents of a GargantuanTable.
// Example:
//    GargantuanTableIterator* iter = table->NewIterator();
//    for (iter->Seek("foo"); !iter->done(); iter->Next()) {
//      process(iter->key(), iter->value());
//    }
//    delete iter;
class GargantuanTableIterator {
  ...
};
```

#### Todo Comment

```cpp
// TODO(kl@gmail.com): Use a "*" here for concatenation operator.
// TODO(Zeke) change this to use relations.
```


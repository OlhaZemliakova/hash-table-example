# hash-table-example

```
class HashTable {
  constructor(size = 100) {
    this.size = size;
    this.table = new Array(size);
  }

  // Simple hash function to convert a string key into an index
  hash(key) {
    let hashValue = 0;
    for (let i = 0; i < key.length; i++) {
      hashValue += key.charCodeAt(i);
    }
    return hashValue % this.size;
  }

  // Insert a key-value pair into the hash table
  insert(key, value) {
    const index = this.hash(key);
    if (!this.table[index]) {
      this.table[index] = [];
    }
    this.table[index].push({ key, value });
  }

  // Retrieve the value associated with a given key
  get(key) {
    const index = this.hash(key);
    const bucket = this.table[index];
    if (bucket) {
      for (const entry of bucket) {
        if (entry.key === key) {
          return entry.value;
        }
      }
    }
    return undefined; // Key not found
  }

  // Remove a key-value pair from the hash table
  remove(key) {
    const index = this.hash(key);
    const bucket = this.table[index];
    if (bucket) {
      this.table[index] = bucket.filter((entry) => entry.key !== key);
    }
  }
}

// Example Usage:
const myHashTable = new HashTable();

myHashTable.insert("name", "John");
myHashTable.insert("age", 25);
myHashTable.insert("city", "New York");

console.log(myHashTable.get("name")); // Output: John
console.log(myHashTable.get("age")); // Output: 25

myHashTable.remove("age");
console.log(myHashTable.get("age")); // Output: undefined (key "age" has been removed)

```

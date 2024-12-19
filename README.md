# Key-Value Store

This project implements a **Key-Value Store** from scratch in Python, optimized for fast insertions and retrievals. It incorporates components like a Write-Ahead Log (WAL), MemTable, Segments, and a Bloom Filter, ensuring durability, efficiency, and scalability.

## Features

- **Write-Ahead Log (WAL):** Guarantees durability by logging all operations to disk.
- **MemTable:** Fast in-memory writes, flushed to disk when full.
- **Log-Structured Segments:** Efficient disk storage with appending operations.
- **Bloom Filter:** Accelerates lookups by filtering non-existent keys.
- **Indexing:** Maps keys to their location in disk segments for quick access.
- **Benchmarking:** Tools to measure performance for various CRUD operations.

## Components

### Write-Ahead Log
- Logs all changes to disk before executing them.
- Provides durability even during unexpected failures.

### MemTable
- In-memory storage for fast key-value operations.
- Periodically flushed to disk segments.

### Log-Structured Segments
- Appends key-value pairs to disk in serialized form.
- Efficient for sequential writes and avoids random disk I/O.

### Bloom Filter
- A probabilistic data structure to quickly test key existence.
- Reduces unnecessary disk reads.

### Indexing
- Maps keys to segment IDs and offsets for retrieval.

## Installation

Install dependencies:

```bash
pip install bloom-filter
```

## Usage

1. Generate synthetic data:

   ```python
   from Data import DataGenerator
   data_file = DataGenerator.generate_data(10000)
   ```

2. Initialize the KVStore:

   ```python
   from MainClass import KVStore
   store = KVStore("./kvstore")
   ```

3. Perform operations:

   ```python
   store.set("key1", "value1")
   value = store.get("key1")
   store.delete("key1")
   ```

4. Benchmark:

   ```python
   from benchmark import Benchmark
   Benchmark.run(store, data_file, 10000)
   ```

5. Close the store:

   ```python
   store.close()
   ```

## Design Choices

The design prioritizes fast CRUD operations with durability and scalability:

1. **Durability:** WAL ensures no data loss.
2. **Efficiency:** MemTable and Bloom Filter accelerate writes and reads.
3. **Scalability:** Log-structured segments manage disk data effectively.

## Repository Structure

- `MainClassipynb`: Core implementation of the KVStore.
- `Benchmark.ipynb`: Benchmarking tools.
- `Data.ipynb`: Synthetic data generator.
- `README.md`: Documentation.

## Benchmark Results

The store processes 30,000 operations (set, get, delete) in ~2 seconds for 10,000 keys.

## Acknowledgment

This project was inspired by the work in [jumpDB](https://github.com/NavyaZaveri/jumpDB).

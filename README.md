# Simple File-based Database using Golang

## Overview

This project is a simple file-based database written in Golang. It stores records as JSON files in a specified directory, providing basic CRUD operations (Create, Read, Update, Delete) on the data. It can be used as a lightweight local storage solution for applications.

## Key Features

   - Store data as JSON files in a directory.
   - Support for creating, reading, and deleting      records.
   - Synchronous file operations with thread safety using mutex locks.
   - Simple logger integration for debugging and tracking database actions.
   - Deletion operations to remove a single entry or all entries from a collection.

## Technology Stack

- **Golang**: The main programming language used to build this database, known for its efficiency, concurrency handling, and simplicity.
- **JSON**: Data is stored as JSON files, making it easy to read and manipulate.
- **Lumber**: A lightweight logger package that logs database actions to the console for debugging.
- **Sync Package**: Golang's `sync.Mutex` is used to handle thread safety during file operations.

## Architecture

This project follows a simple file-based architecture to handle CRUD operations. Here is how the system works:

- **Driver Initialization**
   - The `New()` function initializes the database, creating the specified directory for JSON files if it doesn't exist and setting up optional logging.

- **Thread Safety**
   - Each collection has its own `sync.Mutex` to ensure thread safety. The `getOrCreateMutex()` function manages mutex creation or retrieval for collections.

- **CRUD Operations**
   - **Create/Write**
      : The `Write()` function stores data in JSON format, ensuring atomic writes by renaming temporary files.
   - **Read**
      : The `Read()` function retrieves a single record, while `ReadAll()` reads all records in a collection.

   - **Delete**
      : The `Delete()` function removes a single entry or an entire collection.

- **Error Handling and Logging**
   - Errors are handled gracefully, and logs are generated using the `lumber` package with different levels (DEBUG, INFO, ERROR).

- **File System Storage**
   - Data is stored in JSON files within folders corresponding to collections, ensuring a structured and manageable format.

## Getting Started

### Prerequisites
To run this project, you'll need:
- Golang installed (1.18 or later).
- Basic understanding of Go and JSON handling.

## Run Locally

Clone the repository
```bash
    git clone https://github.com/Srivastava-samarth/go-database.git
    cd go-database
```

Start the server

```bash
  go run main.go
```


## Logging
The project includes a simple logger powered by the `lumber` package. Logs are displayed in the console and track actions like database creation and file operations.

## Deletion Operations
The commented part of the code in the `main.go` file demonstrates two ways to delete records from the database:

- **Delete a single entry** 

   ```bash
   if err := db.Delete("users", "John"); err != nil {
      fmt.Println("Error:", err);
   }
   ```
- **Delete all entries** 

   ```bash
   if err := db.Delete("users", ""); err != nil {
      fmt.Println("Error:", err);
   }
   ```
   ## Contributing

Contributions are always welcome!Please fork the repository and submit a pull request.

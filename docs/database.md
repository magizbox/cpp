# Database

## **Sqlite with Visual Studio 2013**

**Step 1**: Create new project
1.1 Create a new C++ Win32 Console application.

**Step 2:** Download Sqlite DLL

2.1. Download the native SQLite DLL from: http://sqlite.org/sqlite-dll-win32-x86-3070400.zip
2.2. Unzip the DLL and DEF files and place the contents in your project’s source folder (an easy way to find this is to right click on the tab and click the “Open Containing Folder” menu item.

**Step 3:** Build LIB file

3.1. Open a “Developer Command Prompt” and navigate to your source folder. (If you can't find this tool, follow this post in stackoverflow [Where is Developer Command Prompt for VS2013?](http://stackoverflow.com/questions/21476588/where-is-developer-command-prompt-for-vs2013) to create it)
3.2. Create an import library using the following command line: LIB /DEF:sqlite3.def

**Step 4:** Add Dependencies

4.1. Add the library (i.e. sqlite3.lib) to your Project Properties -> Configuration Properties -> Linker -> Input -> Additional Dependencies.
4.2. Download http://sqlite.org/sqlite-amalgamation-3070400.zip
4.3. Unzip the sqlite3.h header file and place into your source directory.
4.4. Include the the sqlite3.h header file in your source code.
4.5. You will need to include the sqlite3.dll in the same directory as your program (or in a System Folder).

**Step 5:** Run test code

```cpp
#include "stdafx.h"
#include <ios>
#include <iostream>
#include "sqlite3.h"

using namespace std;

int _tmain(int argc, _TCHAR* argv[])
{
   int rc;
   char *error;

   // Open Database
   cout << "Opening MyDb.db ..." << endl;
   sqlite3 *db;
   rc = sqlite3_open("MyDb.db", &db);
   if (rc)
   {
      cerr << "Error opening SQLite3 database: " << sqlite3_errmsg(db) << endl << endl;
      sqlite3_close(db);
      return 1;
   }
   else
   {
      cout << "Opened MyDb.db." << endl << endl;
   }

   // Execute SQL
   cout << "Creating MyTable ..." << endl;
   const char *sqlCreateTable = "CREATE TABLE MyTable (id INTEGER PRIMARY KEY, value STRING);";
   rc = sqlite3_exec(db, sqlCreateTable, NULL, NULL, &error);
   if (rc)
   {
      cerr << "Error executing SQLite3 statement: " << sqlite3_errmsg(db) << endl << endl;
      sqlite3_free(error);
   }
   else
   {
      cout << "Created MyTable." << endl << endl;
   }

   // Execute SQL
   cout << "Inserting a value into MyTable ..." << endl;
   const char *sqlInsert = "INSERT INTO MyTable VALUES(NULL, 'A Value');";
   rc = sqlite3_exec(db, sqlInsert, NULL, NULL, &error);
   if (rc)
   {
      cerr << "Error executing SQLite3 statement: " << sqlite3_errmsg(db) << endl << endl;
      sqlite3_free(error);
   }
   else
   {
      cout << "Inserted a value into MyTable." << endl << endl;
   }

   // Display MyTable
   cout << "Retrieving values in MyTable ..." << endl;
   const char *sqlSelect = "SELECT * FROM MyTable;";
   char **results = NULL;
   int rows, columns;
   sqlite3_get_table(db, sqlSelect, &results, &rows, &columns, &error);
   if (rc)
   {
      cerr << "Error executing SQLite3 query: " << sqlite3_errmsg(db) << endl << endl;
      sqlite3_free(error);
   }
   else
   {
      // Display Table
      for (int rowCtr = 0; rowCtr <= rows; ++rowCtr)
      {
         for (int colCtr = 0; colCtr < columns; ++colCtr)
         {
            // Determine Cell Position
            int cellPosition = (rowCtr * columns) + colCtr;

            // Display Cell Value
            cout.width(12);
            cout.setf(ios::left);
            cout << results[cellPosition] << " ";
         }

         // End Line
         cout << endl;

         // Display Separator For Header
         if (0 == rowCtr)
         {
            for (int colCtr = 0; colCtr < columns; ++colCtr)
            {
               cout.width(12);
               cout.setf(ios::left);
               cout << "~~~~~~~~~~~~ ";
            }
            cout << endl;
         }
      }
   }
   sqlite3_free_table(results);

   // Close Database
   cout << "Closing MyDb.db ..." << endl;
   sqlite3_close(db);
   cout << "Closed MyDb.db" << endl << endl;

   // Wait For User To Close Program
   cout << "Please press any key to exit the program ..." << endl;
   cin.get();

   return 0;
}
```

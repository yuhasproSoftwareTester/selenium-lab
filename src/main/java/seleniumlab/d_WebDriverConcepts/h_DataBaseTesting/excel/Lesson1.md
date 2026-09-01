# Apache POI XSSF

## 1. What is Apache POI?

Apache POI is a Java library to read and write Microsoft Office files. XSSF is the component used for Excel files in `.xlsx` format (Excel 2007 and later).

---

## 2. Maven Dependency

Add this to your `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

---

## 3. Core Classes

| Class | What it represents |
|-------|------------------|
| `XSSFWorkbook` | The entire Excel file |
| `XSSFSheet` | A single worksheet (tab) inside the file |
| `XSSFRow` | A horizontal row in the sheet |
| `XSSFCell` | A single cell inside a row |

---

## 4. Creating a New Excel File

```java
import org.apache.poi.xssf.usermodel.*;
import java.io.FileOutputStream;

public class CreateExcel {
    public static void main(String[] args) throws Exception {
        // 1. Create a workbook
        XSSFWorkbook workbook = new XSSFWork();

        // 2. Create a sheet
        XSSFSheet sheet = workbook.createSheet("Students");

        // 3. Create a row at index 
        XSSFRow row = sheet.createRow(0);

        // 4. Create cells and set values
        XSSFCell cell1 = row.createCell(0);
        cell1.setCellValue("Name");

        XSSFCell cell2 = row.createCell(1);
        cell2.setCellValue("Marks");

        // 5. Add data in row 1
        XSSFRow dataRow = sheet.createRow(1);
        dataRow.createCell(0).setCellValue("Alice");
        dataRow.createCell(1).setCellValue(85);

        // 6. Save to file
        FileOutputStream fos = new FileOutputStream("students.xlsx");
        workbook.write(fos);

        // 7. Close resources
        fos.close();
        workbook.close();

        System.out.println("File created successfully.");
    }
}
```

---

## 5. Reading an Existing Excel File

```java
import org.apache.poi.xssf.usermodel.*;
import java.io.FileInputStream;

public class ReadExcel {
    public static void main(String[] args) throws Exception {
        FileInputStream fis = new FileInputStream("students.xlsx");
        XSSFWorkbook workbook = new XSSFWorkbook(fis);
        XSSFSheet sheet = workbook.getSheetAt(0); // get first sheet

        // Loop through rows
        for (Row row : sheet) {
            for (Cell cell : row) {
                switch (cell.getCellType()) {
                    case STRING:
                        System.out.print(cell.getStringCellValue() + "\t");
                        break;
                    case NUMERIC:
                        System.out.print(cell.getNumericCellValue() + "\t");
                        break;
                    default:
                        System.out.print("UNKNOWN\t");
                }
            }
            System.out.println();
        }

        workbook.close();
        fis.close();
    }
}
```

---

## 6. Cell Types

| Type | Method to read | Method to write |
|------|---------------|-----------------|
| String | `getStringCellValue()` | `setCellValue(String)` |
| Number | `getNumericCellValue()` | `setCellValue(double)` |
| Boolean | `getBooleanCellValue()` | `setCellValue(boolean)` |
| Formula | `getCellFormula()` | `setCellFormula(String)` |
| Blank | `getCellType() == CellType.BLANK` | - |

---

## 7. Formulas

```java
XSSFRow row = sheet.createRow(2);
XSSFCell formulaCell = row.createCell(1);
formulaCell.setCellFormula("SUM(B1:B:B2)");
```

---

## 8. Auto-sizing Columns

```java
sheet.autoSizeColumn(0); // auto-fit column 0
sheet.autoSizeColumn(1); // auto-fit column 1
```

---

## 9. Common Tips

- Always close `Workbook`, `FileInputStream`, and `FileOutputStream` to avoid memory leaks.
- Row and cell indices start from 0.
- Use `try-with-resources` for automatic closing:

```java
try (XSSFWorkbook wb = new XSSFWorkbook();
     FileOutputStream fos = new FileOutputStream("file.xlsx")) {
    // your code here
}
```

---

## 10. Common Exception

| Exception | Cause |
|-----------|-------|
| `FileNotFoundException` | File path is wrong or file is open in Excel |
| `IOException` | Problem reading/writing the file |
| `IllegalStateException` | Trying to read a number cell as string |

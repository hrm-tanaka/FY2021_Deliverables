    /**
     * Excelファイルを読み込みます
     *
     * @return 
     */
    public List<String[]> readAll() throws IOException {
        List<String[]> results = new ArrayList<>();
        Workbook wb = new XSSFWorkbook(filePath);
        //1番目のシートを読み込む
        Sheet sh = wb.getSheetAt(0);
        Iterator<Row> rowIterator = sh.rowIterator();
        
        while (rowIterator.hasNext()) {
            Row row = rowIterator.next();
            String[] record = new String[row.getLastCellNum()];
            Iterator<Cell> cellIterator = row.cellIterator();
            while (cellIterator.hasNext()) {
                Cell cell = cellIterator.next();
                record[cell.getColumnIndex()] = cell.getStringCellValue();
            }

        }
        return results;
    }

    /**
     * Excelファイルを読み込みます
     *
     * @return 業者一覧
     */
    public List<String[]> readAll() throws IOException {
        List<String[]> results = new ArrayList<>();
        Workbook wb = new XSSFWorkbook(filePath);
        //1番目のシートを読み込む
        Sheet sh = wb.getSheetAt(0);
        Iterator<Row> rowIterator = sh.rowIterator();
        while (rowIterator.hasNext()) {
            Row row = rowIterator.next();
            // ヘッダー行は無視するため、4行目から始める
            if (row.getRowNum() < 3) {
                continue;
            }
            String[] record = new String[row.getLastCellNum()];
            Iterator<Cell> cellIterator = row.cellIterator();
            while (cellIterator.hasNext()) {
                Cell cell = cellIterator.next();
                record[cell.getColumnIndex()] = cell.getStringCellValue();
            }
            if (!Arrays.stream(record).allMatch(StringUtils::isBlank)) {
                results.add(record);
            }
        }
        return results;
    }


# Datasets

This folder contains datasets and Power BI reports used in the Fabric Data Agent Gallery. It contains Power BI semantic model/report (.pbix) and their corresponding data source files.:

## ⚙️ How to Use (Example)

1. **Download the Files**
   - [Download Office Supplies Retail Performance - AI Ready2.pbix](./Office%20Supplies%20Retail%20Performance%20-%20AI%20Ready2.pbix)
   - [Download office_supplies_star_schema_data.xlsx](./office_supplies_star_schema_data.xlsx)

2. **Open the PBIX File**
   - Launch Power BI Desktop.
   - Open the `Office Supplies Retail Performance - AI Ready2.pbix` file.

3. **Update the Data Source Path**
   - In Power BI Desktop, go to the **Home** tab and click on **Transform data**.
   - In the Power Query Editor, locate the **_FilePath** parameter.
   - Update the value of `_FilePath` to the full path where you saved the `office_supplies_star_schema_data.xlsx` file on your local machine.
   - Click **Close & Apply** to refresh the data.

Once the data is refreshed, the report visuals will be updated with the data from your local Excel file.

---

For any issues or questions, feel free to open an [issue](https://github.com/your-org/fabric-data-agent-gallery/issues).

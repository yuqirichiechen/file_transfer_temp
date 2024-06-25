private void btnConvertToPDF_Click(object sender, EventArgs e)
{
    try
    {
        // Load the DOCX documents and convert them to PDF
        Spire.Doc.Document doc1 = new Spire.Doc.Document();
        doc1.LoadFromFile(file1Path);
        string pdf1Path = Path.ChangeExtension(file1Path, ".pdf");
        doc1.SaveToFile(pdf1Path, Spire.Doc.FileFormat.PDF);

        Spire.Doc.Document doc2 = new Spire.Doc.Document();
        doc2.LoadFromFile(file2Path);
        string pdf2Path = Path.ChangeExtension(file2Path, ".pdf");
        doc2.SaveToFile(pdf2Path, Spire.Doc.FileFormat.PDF);

        // Use Spire.Pdf to load and merge the PDF documents
        Spire.Pdf.PdfDocument finalPdf = new Spire.Pdf.PdfDocument();
        finalPdf.LoadFromFile(pdf1Path);
        finalPdf.AppendPage(pdf2Path);

        // Save the merged PDF
        SaveFileDialog saveFileDialog = new SaveFileDialog();
        saveFileDialog.Filter = "PDF files (*.pdf)|*.pdf";
        saveFileDialog.DefaultExt = "pdf";
        if (saveFileDialog.ShowDialog() == DialogResult.OK)
        {
            finalPdf.SaveToFile(saveFileDialog.FileName);
            MessageBox.Show("PDFs merged and saved successfully!");
        }

        finalPdf.Close(); // Ensure to close the document to release resources
    }
    catch (Exception ex)
    {
        MessageBox.Show("Failed to convert or merge PDFs: " + ex.Message);
    }
}

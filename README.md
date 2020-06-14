# DunamicPHPCertificate
<?php
require('fpdf.php');

$pdf = new FPDF();
$pdf->AddPage();
$pdf->SetFont('Arial','B',16);
$pdf->Cell(40,10,'Hello World!');
$pdf->Output();
?>
[Demo]

After including the library file, we create an FPDF object. The constructor is used here with the default values: pages are in A4 portrait and the unit of measure is millimeter. It could have been specified explicitly with:
$pdf = new FPDF('P','mm','A4');
It's possible to use landscape (L), other page sizes (such as Letter and Legal) and units (pt, cm, in).

There's no page at the moment, so we have to add one with AddPage(). The origin is at the upper-left corner and the current position is by default set at 1 cm from the borders; the margins can be changed with SetMargins().

Before we can print text, it's mandatory to select a font with SetFont(). We choose Arial bold 16:
$pdf->SetFont('Arial','B',16);
We could have specified italics with I, underlined with U or a regular font with an empty string (or any combination). Note that the font size is given in points, not millimeters (or another user unit); it's the only exception. The other standard fonts are Times, Courier, Symbol and ZapfDingbats.

We can now print a cell with Cell(). A cell is a rectangular area, possibly framed, which contains a line of text. It is output at the current position. We specify its dimensions, its text (centered or aligned), if borders should be drawn, and where the current position moves after it (to the right, below or to the beginning of the next line). To add a frame, we would do this:
$pdf->Cell(40,10,'Hello World !',1);
To add a new cell next to it with centered text and go to the next line, we would do:
$pdf->Cell(60,10,'Powered by FPDF.',0,1,'C');
Remark: the line break can also be done with Ln(). This method additionnaly allows to specify the height of the break.

Finally, the document is closed and sent to the browser with Output(). We could have saved it to a file by passing the appropriate parameters.

Caution: in case when the PDF is sent to the browser, nothing else must be output by the script, neither before nor after (no HTML, not even a space or a carriage return). If you send something before, you will get the error message: "Some data has already been output, can't send PDF file". If you send something after, the document might not display.

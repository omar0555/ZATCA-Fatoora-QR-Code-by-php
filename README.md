# ZATCA-Fatoora-QR-Code-by-php
 An unofficial package maintained by Salla to help developers to implement ZATCA (Fatoora) QR code easily which required for e-invoicing by php
 

<?PHP
//print  QR-CODE
include 'phpqrcode/qrlib.php';
$fileQR = ".png";
$ecc = 'L';
$pixel_Size = 10;
$frame_Size = 10;

$sellername='إسم المنشأة';
$taxno='الرقم الضريبي الخاص بالمنشأة';
$date='تاريخ ووقت إنشاء الفاتورة';
$Grandtotal='المجموع الكلي للفاتورة بعد الضريبة';
$vat='قيمة الضريبة';

$barcode=getbarcode($sellername,$taxno,$date,$Grandtotal,$vat);

QRcode::png($barcode, $fileQR, $ecc, $pixel_Size);

?>
<img src='<?php echo $fileQR ?>' style='width: 150px;'  title='QR-code' >








<?php
//function TLV ZATKA 
function getbarcode($sellername,$taxno,$date,$Grandtotal,$vat){
$tag1 = pack('H*', sprintf("%02X",1));
$length1 = pack('H*', sprintf("%02X",strlen($sellername)));
$value1=$sellername;

$tag2 = pack('H*', sprintf("%02X",2));
 $length2 = pack('H*', sprintf("%02X",strlen($taxno)));
$value2=$taxno;

$tag3 = pack('H*', sprintf("%02X",3));
 $length3 = pack('H*', sprintf("%02X",strlen($date)));
$value3=$date;

$tag4 = pack('H*', sprintf("%02X",4));
 $length4 = pack('H*', sprintf("%02X",strlen($Grandtotal)));
$value4=$Grandtotal;

$tag5 = pack('H*', sprintf("%02X",5));
 $length5 = pack('H*', sprintf("%02X",strlen($vat)));
$value5=$vat;

return base64_encode($tag1.$length1.$value1.$tag2.$length2.$value2.$tag3.$length3.$value3.$tag4.$length4.$value4.$tag5.$length5.$value5);
}

?>



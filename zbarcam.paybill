#!/bin/bash

tmp=/tmp/barcode
zbarcam > $tmp &
pid=$!

while [[ ! -s $tmp ]] ; do
    sleep 1
done

kill $pid

barcode=$(cat $tmp)
rm $tmp

barcode=${barcode:9}

bill_type=${barcode:11:1}
bill_id="$(echo ${barcode:0:13} | sed 's/^0*//')"
pay_id="$(echo ${barcode:13:13} | sed 's/^0*//')"
amount="$(echo ${barcode:13:8} | sed 's/^0*//')000"

echo "Barcode: $barcode"
echo "Bill Type: $bill_type"
echo "Bill ID: $bill_id"
echo "Pay ID: $pay_id"
echo "Amount: $amount"

case "$bill_type" in

1)
    bill_type="آب"
    ;;
2)
    bill_type="برق"
    ;;
3)
    bill_type="گاز"
    ;;
4)
    bill_type="تلفن ثابت"
    ;;
5)
    bill_type="تلفن همراه"
    ;;
6)
    bill_type="شهرداری"
    ;;
*)
    bill_type="قبض نامعتبر"
    ;;
esac

zenity --info --title="مشحصات قبض $bill_type" --text="شناسه قبض: $bill_id\n\nشناسه پرداخت: $pay_id\n\nمبلغ قابل پرداخت: $amount ریال"

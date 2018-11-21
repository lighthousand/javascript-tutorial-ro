În general folosim upper case pentru constante care sunt "hard-codate" (hard-coded). Sau cu alte cuvinte când valoarea este cunoscută dinainte de execuție și este scrisă direct în cod.

În acest cod `birthday` este exact așa. Așa că am putea folosi upper case pentru aceasta.

În contrast, `age` este evaluată la run-time. Astăzi avem o vârstă, peste un an vom avea alta. Este constantă într-un sens, acela că nu se modifică pe parcursul execuției codului. Dar este "mai puțin constantă" decât `birthday`, este calculată, așa că ar trebui să păstrăm lower case pentru aceasta.
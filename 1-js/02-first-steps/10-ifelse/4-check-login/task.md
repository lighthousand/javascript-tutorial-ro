importanță: 3

---

# Verifică login-ul

Scrie cod care așteaptă un login cu `prompt`.

Dacă vizitatorul introduce `"Admin"`, atunci afișează `prompt` pentru parolă, dacă input-ul este o linie goală sau `key:Esc` -- afișează "Canceled.", dacă este alt string -- atunci afișează "Nu te cunosc".

Parola este verificată după cum urmează:

- Dacă este egală cu "TheMaster", atunci afișează "Welcome!",
- Alt string -- afișează "Parolă greșită",
- Pentru un string gol sau input anulat, afișează "Canceled."

Schema:

![](ifelse_task.png)

Te rog folosește blocuri imbricate `if`. Ai grijă la lizibilitatea globală a codului.

Indiciu: transmiterea unui input gol către un prompt returnează un string gol `''`. Apăsarea tastei `key:ESC` în timpul unui prompt returnează `null`.

[demo]

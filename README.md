# Gestione dei database

**Visualizzare i databases:**
``` sql
SHOW DATABASES;
```

**Creare un database:**
``` sql
CREATE DATABASE {NomeDB};
```

**Usare un database:**
``` sql
USE {NomeDB};
```

# Tabelle

### Gestione tabelle

**Creare una tabella:**
``` sql
CREATE TABLE {NomeTabella} (
	{NomeCampo} {TipoAttributo} {Parametri},
	PRIMARY KEY ({NomeCampo}),
	FOREIGN KEY ({NomeCampo}) REFERENCES {NomeTabella}({NomeCampo})
);
```

**Rimuovere una tabella:**
``` sql
DROP TABLE {NomeTabella};
```

**Lista tipi attributi:**
* INT
* VARCHAR(n)
* DECIMAL(15,2)
* ...

**Lista parametri:**
* NULL
* NOT NULL
* AUTO_INCREMENT

### Modifiche ai campi

**Cambiare nome ad una tabella:**
``` sql
ALTER TABLE {NomeTabella} RENAME {NuovoNome};
```

**Cambiare nome e tipo di un campo:**
``` sql
ALTER TABLE {NomeTabella} CHANGE {VecchioNomeCampo} {NuovoNomeCampo} {NuovoTipoCampo};
```

**Aggiungere un campo:**
``` sql
ALTER TABLE {NomeTabella} ADD {NomeCampo} {TipoCampo};
```

**Rimuovere un campo:**
``` sql
ALTER TABLE {NomeTabella} DROP {NomeCampo};
```

### Gestione elementi

**Inserire un elemento:**
``` sql
INSERT INTO {NomeTabella} VALUES ([Val1], [Val2], ...);
```

**Aggiornare un campo:**
``` sql
UPDATE {NomeTabella} SET {NomeCampo} = {Valore} WHERE id = {Valore};
```

**Rimuovere un elemento:**
``` sql
DELETE FROM {NomeTabella} WHERE id = {Valore};
```

# Query

**Visualizzare tutti gli elementi di una tabella:**
``` sql
SELECT *
	FROM {NomeTabella};
```

**Join esplicito:**
``` sql
SELECT *
	FROM Tab1
	JOIN Tab2 ON Tab1.ID = Tab2.COD_Tab1;
```

**Join implicito:**
``` sql
SELECT *
	FROM Tab1, Tab2
		WHERE Tab1.ID = Tab2.COD_Tab1;
```

**Prodotto cartesiano:**
``` sql
SELECT *
	FROM Tab1, Tab2;
```

# Funzione di aggregazione

Elenco funzioni:
* MAX
* MIN
* SUM
* AVG
* COUNT
	* Non conta i valori nulli

I raggruppamenti possono essere anche multipli (es. Numero dipendenti per sede e città)

CLAUSALA HAVING

CLAUSOLA ORDER BY per mettere in ordine

**Esempio sintassi:**

**Somma degli stipendi della sede S01:**
``` sql
SELECT SUM(Stipendio) AS TotStipendio
	FROM Impiegati
		WHERE Sede='S01';
```

**Somma degli stipendi annui della sede S01:**
``` sql
SELECT SUM(Stipendio*12) AS TotStipendioAnnuo
	FROM Impiegati
		WHERE Sede='S01';
```

**Impiegati nella sede S1:**
``` sql
SELECT Count(*) AS NumeroImpiegati
	FROM Impiegati
		WHERE Sede='S01';
```

**Media degli stipendi di ogni sede:**
``` sql
SELECT Sede, AVG(Stipendio) AS MediaStipendio
	FROM Impiegati
		GROUP BY Sede;
```

**Visualizzare il numero degli impiegati per ciascuna sede ma con le sede che hanno più di 2 impiegati:**
``` sql
SELECT Sede COUNT(*) AS NumeroImpiegati
	FROM Impiegati
		GROUP BY Sede
			HAVING COUNT(*) > 2;
```

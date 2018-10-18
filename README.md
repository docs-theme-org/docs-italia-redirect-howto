# Come gestire i redirect dai documenti ReadTheDocs a Docs Italia

## Selezionare il repo ufficiale

* Scegliere il documento di cui creare il redirect dalla [lista dei Documenti da spostare](https://github.com/docs-theme-org/docs-italia-redirect-howto/projects/1) e spostare `in-progress` (es: `guida-docs-italia`)
* Clonarne in locale il repo dall'organizzazione `italia` (es: ` git clone git@github.com:italia/docs-italia-guide.git`)

## Modificare il repo ufficiale e creare una copia nell'organizzazione `docs-theme-org`

* Rimuovere link al remote originale `git remote rm origin`
* Aggiungere `conf.py`
* Aggiungere cartella `redirect_template` con i due file
* Aggiungere `redirect.yml` *e modificarlo con i dati corretti*
* Creare un repo *con lo stesso nome* dentro org `docs-theme-org`
* `git add . && git commit -m "Redirection template added"`
* `git remote add origin git@github.com:docs-theme-org/nome.git` (es: `git remote add origin git@github.com:docs-theme-org/docs-italia-guide.git`)
* `git push -u origin master`

## Creare un progetto ReadTheDocs temporaneo per testare il redirect

* Creare nuovo progetto con nome uguale al progetto ReadTheDocs originale, ma con suffisso `-redirect` (es: `guida-docs-italia-redirect`)
* Nelle impostazioni avanzate, selezionare la lingua corretta (tipicamente Italiano)
* Associarvi il repo appena creato e compilare tutte le versioni necessarie

## Verificare che il redirect funzioni

* Clonare il repo `docs-theme-org\docs-italia-redirect-checker` e *modificarne `document_redirects.yml` con i dati necessari* (versioni e URL)
* Lanciare `python check_redirects.py`
* Il tool verificherà che ad ogni URL del repository di test corrisponda un URL su Docs Italia

## Concludere associando il nuovo repo con il progetto ufficiale su ReadTheDocs

* Modificare nel progetto RTD ufficiale il repo "sorgente" da quello originale a quello con i file per il redirect (es: da https://github.com/italia/docs-italia-guide a https://github.com/docs-theme-org/docs-italia-guide)
* Lanciare la build di tutte le versioni e verificare che funzioni (es: https://guida-docs-italia.readthedocs.io/it/latest/ re-indirizzi su https://docs.italia.it/italia/docs-italia/docs-italia-guide/it/bozza/)
* Rimuovere il progetto ReadTheDocs temporaneo (quello con suffisso `-redirect`)
* Aggiornare la [lista dei Documenti da spostare](https://github.com/docs-theme-org/docs-italia-redirect-howto/projects/1) spostando il documento in `done`.

## Quotes Database Interface

The Quotes Interface is a way to quickly access a Chirpy-based QDB.

### Usage

    !quote add <quote>               : Submits a quote to the database.  This is best for one-line quotes
    !quote addlast <number>          : Adds the last <number> lines as a quote.
    !quote remember <nick> <snippet> : Saves and submits the last one-liner from <nick> that includes the words <snippet>
    !quote get <number>              : Retrieves and sends the quote with id <number>.

Also available within this module is an XKCDB scraper:

    !xkcdb <number>

Where number is an XKCDB quote number.

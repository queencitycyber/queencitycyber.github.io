**Metagoofil**

Another powerful searching tool written in Python that is used to extract metadata from files and documents from our target. Metagoofil will use pre built google dorks \(the same ones we went over\) to download different document and images types, and then using metadata libraries such as Hachoir, PDFMiner, Meta Data Extraction tool, and others, that will extract different pieces of metadata from those files. The results can then be saved and reports generated for custom output options. The reports will include usernames, software and versions, machine names, and other information that will help keep our work organized.

Lets start the tool with the simple command `metagoofil`

As we can see from the options, let build a command to gather as much information as we can, point it at our target domain, and generate an HTML report.

The command we will use is metagoofil –d ericonsecurity.com –t pdf,doc,xls,ppt,odp,docx,xlsx,pptx –f results.html

Since we were not able to extract any useful with our own private domain, here are some screenshots of the generated reports from the homepage of the tool \([https://code.google.com/p/metagoofil/](https://code.google.com/p/metagoofil/)\)



All of this information should be added to your organized notes!


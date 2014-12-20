read_gbfile
===========

from Bio import Entrez
from Bio import SeqIO
#abrir o ficheiro
Entrez.email = 'example@hotmail.com'
handle = Entrez.efetch(db="nucleotide", rettype="gb", retmode="text",id="52840256", seq_start="0", seq_stop='248700' )
seq_record = SeqIO.read(handle, "gb")

#Guardar
SeqIO.write(seq_record, 'sequence.gb', "genbank")
handle.close()

#Teste
record = SeqIO.read("sequence.gb", "genbank")
print record


print "Features:"
print len(record.features) #numero de features totais

featcds = []
featgene=[]
for i in xrange(len(record.features)): 
    if record.features[i].type == "CDS": 
        featcds.append(i)
    if  (record.features[i].type == "gene"):
        featgene.append(i)
        i=+1
print 'Numero de features CDS: ' + str(len(featcds))
print 'Numero de features Gene: ' + str(len(featgene))

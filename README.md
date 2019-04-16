# PythonGraphPlot
For Plotting Graph between Ack/Seq and Time. The Acknowledgements coming from Receiver and Data Seq Numbers from Sender side are plotted between Ack/Seq and Time
###This code is for AckSeq vs Time
from scapy.all import *
import matplotlib.pyplot as plt
pkts=rdpcap("/home/ackseq_file.pcap")
l=len(pkts)

x=[]
y=[]
p=[]
q=[]
m=[]
n=[]
for pkt in pkts:
	if pkt[IP].src=='192.168.102.100': # Receiver side Acknowledgements
	   a=pkt.time-pkts[0].time
	   x.append(a)
	   b=pkt.ack
	   y.append(b)

for i in y:
	   i=i-y[0]
           m.append(i)

for pkt in pkts:
	if pkt[IP].src=='192.168.102.101': #Sender side Sequence Numbers
	   c=pkt.time-pkts[0].time
	   p.append(c)
	   d=pkt.seq
	   q.append(d)
for j in q:
	   j=j-q[0]
           n.append(j)

plt.scatter(x,m,color="r",label="ack")
plt.scatter(p,n,color="b",label="seq")

plt.ticklabel_format(style='plain')
plt.xlabel('Time')
plt.ylabel('Seq/Ack')
plt.title('Graph')
plt.legend(loc='lower left', bbox_to_anchor= (0.0, 1.01), ncol=2, borderaxespad=0, frameon=False)
plt.show()

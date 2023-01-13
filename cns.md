# cns

1.import java.util.Scanner;
public class crc 
{
static int data[],cs[];
static int g[]={1,0,0,0,1,0,0,0,0,0,0,1,0,0,0,0,1};
static int a, i, c;
static int N=17;
void xor() 
{
 for(c=1;c<N;c++) cs[c]=((cs[c]==g[c])?0:1);
}
void crc() 
{
for(i=0;i<N;i++) cs[i]=t[i];
do 
{
 if(cs[0]==1) xor();
 for(c=0;c<N-1;c++) cs[c]=cs[c+1];
 cs[c]=data[e++];
}while(e<=a+N-1);
}
public static void main(String[] args) 
{
cs=new int[100];
crc c1=new crc();
int n;
Scanner br=new Scanner(System.in);
System.out.println("enter no of bits");
n=br.nextInt();
data=new int[100];
System.out.println("\nEnter the data bits : "); 
for(int i=0;i<n;i++)
data[i]=br.nextInt();

System.out.println("\nCRC Divisor : ");
for(int i=0;i<N;i++)
System.out.print(g[i]);
 for(i=n;i<n+N-1;i++) 
data[i]=0;
 
System.out.println("\nModified Data is : ");
for(i=0;i<n+N-1;i++)
System.out.print(data[i]); 
 c1.crc();
 System.out.println("\nCRC Checksum is : ");
 for(int i=0;i<N-1;i++)
System.out.print(cs[i]);
 for(i=n;i<n+N-1;i++) 
data[i]=cs[i-n];
 System.out.println("\nFinal Codeword is :");
 for(i=0;i<n+N-1;i++)
System.out.print(data[i]); 
System.out.println("\nTest Error detection 0(yes) 1(no) ? : ");
 e=br.nextInt();
 if(e==0)
 {
System.out.println("Enter position where error is to inserted : ");
 pos=br.nextInt();
 data[pos]=(data[pos]==0)?1:0;
 
 System.out.println("Errorneous data : ");
 for(i=0;i<n+N-1;i++)
System.out.print(data[i]); 
 }
 c1.crc();
for(i=0;i<N-1;i++)
{
if(cs[i]!=0)
{
System.out.println("Error Data");
System.exit(0);
}
}
System.out.println("No Error");
}
}



2.import java.util.*;
class DVT
{
public static void main(String args[])
{
int dist[][]=new int[20][20];
int from[][]=new int[20][20];
int costmat[][]=new int[10][10];
int i,j,k,nodes;

Scanner s=new Scanner(System.in);
System.out.println("\nEnter the number of nodes : ");
nodes=s.nextInt();
System.out.println("\nEnter the cost matrix :\n");
for(i=1;i<=nodes;i++)
{
for( j=1;j<=nodes;j++)
{
costmat[i][j]=s.nextInt();
costmat[i][i]=0;
dist[i][j]=costmat[i][j];
from[i][j]=j;
}
}
for( i=1;i<=nodes;i++)
{
for( j=1;j<=nodes;j++)
{
for( k=1;k<=nodes;k++)
{ 
if((dist[i][j])>dist[i][k]+dist[k][j])
{ 
dist[i][j]=dist[i][k]+dist[k][j];
from[i][j]=k;
}
}
}
}
for( i=1;i<=nodes;i++)
{
System.out.println("\n\nFrom Router Node :"+i);
 System.out.println("\nDesti Node\tNext Hop\tdistance\n");
for( j=1;j<=nodes;j++)
{
System.out.println(j +"\t \t " +from[i][j]+" \t\t "+dist[i][j]);
}
}
System.out.println("\n\n");
}
}




3.
Server Program:
import java.net.*; 
import java.io.*;
public class ContentsServer 
{
 public static void main(String args[]) throws Exception
 { 

 ServerSocket sersock = new ServerSocket(4000);
 System.out.println("Server ready for connection");
 Socket sock = sersock.accept(); 
System.out.println("Connection is successful and wating for chatting");
 
 
 InputStream istream = sock.getInputStream( );
BufferedReader fileRead =new BufferedReader(new InputStreamReader(istream));
 String fname = fileRead.readLine( );
 
BufferedReader contentRead = new BufferedReader(new FileReader(fname) );
 
 
 OutputStream ostream = sock.getOutputStream( );
 PrintWriter pwrite = new PrintWriter(ostream, true);
 
 String str;

 while((str = contentRead.readLine()) != null) 
{
pwrite.println(str); 
 }
 System.out.println(“Contents of the file is sent…”);
 sock.close(); sersock.close(); 

 pwrite.close(); fileRead.close(); contentRead.close();
 }
Client Program:
import java.net.*;
import java.io.*;
public class ContentsClient 
{
 public static void main( String args[ ] ) throws Exception
 {
 Socket sock = new Socket( "127.0.0.1", 4000);
 
 System.out.print("Enter the file name");
BufferedReader keyRead = new BufferedReader(new 
InputStreamReader(System.in));
 String fname = keyRead.readLine();
 
 OutputStream ostream = sock.getOutputStream( );
 PrintWriter pwrite = new PrintWriter(ostream, true);
 pwrite.println(fname); 
 

System.out.println(“Contents of the File:”);
 InputStream istream = sock.getInputStream();
BufferedReader socketRead = new BufferedReader(new 
InputStreamReader(istream));
 String str;
 while((str = socketRead.readLine()) != null) 

 { 
 System.out.println(str); 
 } 
 pwrite.close(); socketRead.close(); keyRead.close();
 }
}






4.Server Program:

import java.net.*; 
import java.util.*; 
public class DSender
{ 
 public static void main(String[] args) throws Exception 
{ 
 DatagramSocket ds = new DatagramSocket(); 
 Scanner s=new Scanner(System.in); 
System.out.println("Enter the Message and press ENTER to Send");
String str = s.nextLine();
 InetAddress ip = InetAddress.getByName("127.0.0.1"); 
 
DatagramPacket dp = new DatagramPacket(str.getBytes(), str.length(), ip, 21); 
 ds.send(dp); 
 ds.close(); 
 } 
} 
Client Program:

import java.net.*; 
public class DReceiver
{ 
public static void main(String[] args) throws Exception 
{ 
 DatagramSocket ds = new DatagramSocket(21); 
 byte[] buf = new byte[1024]; 
DatagramPacket dp = new DatagramPacket(buf, 1024); 
 ds.receive(dp); 
String str = new String(dp.getData(), 0, dp.getLength());
 System.out.println("Message from Server:"); 
 System.out.println(str); 
 ds.close(); 
}
}






5.import java.util.*;
import java.io.*; 
class RSA
{
static int mult(int x, int y, int n) 
{
 int k=1;
 int j;
for (j=1; j<=y; j++) k = (k * x) % n;
 return ( int) k;
}
public static void main (String arg[])throws Exception
{
Scanner s=new Scanner(System.in); 
InputStreamReader r=new InputStreamReader(System.in); 
BufferedReader br=new BufferedReader(r); 
String msg1;
int pt[]=new int[100];
int ct[]=new int[100];
int a,b, n, d, e,Z, p, q, i,temp,et;
System.out.println("Enter prime No.s p,q :");
p=s.nextInt();
q=s.nextInt();
n = p*q;
Z=(p-1)*(q-1);
System.out.println("\nSelect e value:");
e=s.nextInt();
System.out.printf("Enter message : ");
msg1=br.readLine();
char msg[]=msg1.toCharArray(); 
for(i=0;i<msg.length;i++)
 pt[i]=msg[i];
for(d=1;d<Z;++d)
if(((e*d)%Z)==1) break;
System.out.println("p="+" 
"+p+"\tq="+q+"\tn="+n+"\tz="+Z+"\te="+e+"\td="+d);
 System.out.println("\nCipher Text = ");
 for(i=0; i<msg.length; i++) 
ct[i] = mult(pt[i], e,n);
for(i=0; i<msg.length; i++) 
System.out.print("\t"+ct[i]);
 System.out.println("\nPlain Text = ");
 for(i=0; i<msg.length; i++) 
 pt[i] = mult(ct[i], d,n) ;
 for(i=0; i<msg.length; i++)
System.out.print((char)pt[i]);
}
}







6.import java.util.*;
class LB
{
static int bkt;
static void bktInput(int a,int b)
{
if(a>bkt)
{
System.out.println("Bucket overflow and packet is rejected\n");
Exit(0);
}
else
{
while(a>b)
{
System.out.println("The Bytes Outputed are :"+b);
a-=b;
}
if (a>0)
{
System.out.println("The remaining bytes are :"+a);
System.out.println("Last Bytes Sent :"+a);
System.out.println("Bucket output are successful\n");
}
}
}
public static void main(String arg[])
{
int op, pktSize,i,N;
Scanner s=new Scanner(System.in);
System.out.print("Enter bucket size :");
bkt=s.nextInt();
System.out.print("Enter output rate :");
op=s.nextInt();
Random randomGenerator = new Random();
System.out.println("Enter the No. of packets to be generated");
N=s.nextInt(); 
for( i=1;i<=N;i++)
{
pktSize=randomGenerator.nextInt(100);
System.out.println("\nIncoming packet No:"+" "+i+" and packet size 
is: "+pktSize);
bktInput(pktSize,op);
}}

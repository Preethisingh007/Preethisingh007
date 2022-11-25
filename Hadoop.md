- 👋 Hi, I’m @Preethisingh007
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Preethisingh007/Preethisingh007 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

ls       #to list the files
mkdir    #to create a directry
cd       #to change directry 
history    #to get the history of codes typed
quit       #to quit the previous program
hadoop fs -mkdir preethi      #to create a directr in hadoop
hadoop fs -ls       #to list the files in hadoop
cd Desktop 
ls 
hadoop fs -copyFromLocal /home/cloudera/Desktop/emp.csv preethi/emp.csv     #to copy file into Hadoop file system
hadoop fs -ls preethi

pig        #to go inside the pig
A = load '/user/cloudera/preethi/emp.csv' using PigStorage(',') as (eid:int, ename:chararray, epos:chararray, esal:int, ecom:int,edpno:int);
B = filter A by esal>=1500;
B = filter A by epos=='ANALYST';
B = filter A by epos=='ANALYST' and ename=='SCOTT';
B = limit A 5        # get first five rows
B = order A by eid;
B = order A by eid desc;          #to print rows in desending order
B = filter A by epos=='ANALYST';  #only ANALYSTname people will be there
store B into '/user/cloudera/preethi/pigout' using PigStorage(',');
B = filter A by esal>=1500;

#wordcount in pig
vi text      #to create a file for typing the text
ls      #to see where the text file is
hadoop fs -copyFromLocal home/cloudera/Desktop/text preethi/wordcount       #to import the file from destop to hadoop fs
hadoop fs -ls preethi       #to see whether the file is stored in preethi or not

grunt>A = load 'wordcount' as (line:chararray);
           dump A;
      token = foreach A generate TOKENIZE(line);
      dump token;
      flat = foreach token generate FLATTEN($0);
      dump flat;
      groups = group flat by $0;  
      dump groups;
      wc = foreach groups generate $0 as word, COUNT($1) as freq;
      dump wc;

#hive
create table emp (eid int, ename string, epos string, esal int, ecom int, edpno int) row format delimited fields terminated by ',';
load data local inpath '/home/cloudera/Desktop/emp.csv' into table emp;
select * from emp;
create table if not exists emp ();
create external table extemp (eid int, ename string, epos string, esal int, ecom int, edpno int) 
             row format delimited fields terminated by',' location '/user/cloudera/preethi/external_table';
quit          #quit hive
[cloudera@quickstart Desktop]$ hadoop fs - ls preethi      #after typing this preethi/external_table 

#then go to pig
pig
pwd
grunt>cd preethi 
      cat external_table



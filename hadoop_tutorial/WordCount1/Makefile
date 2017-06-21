run: jar
	hadoop fs -rm -f -r  /user/cloudera/wordcount/output
	hadoop jar wordcount.jar org.myorg.WordCount /user/cloudera/wordcount/input /user/cloudera/wordcount/output

run_caseSensitive: jar
	hadoop fs -rm -f -r  /user/cloudera/wordcount/output
	hadoop jar wordcount.jar org.myorg.WordCount -Dwordcount.case.sensitive=true /user/cloudera/wordcount/input /user/cloudera/wordcount/output 

run_stopwords: jar stopwords
	hadoop fs -rm -f -r  /user/cloudera/wordcount/output
	hadoop jar wordcount.jar org.myorg.WordCount /user/cloudera/wordcount/input /user/cloudera/wordcount/output -skip /user/cloudera/wordcount/stop_words.text

compile: build/org/myorg/WordCount.class

jar: wordcount.jar

wordcount.jar: build/org/myorg/WordCount.class
	jar -cvf wordcount.jar -C build/ .

build/org/myorg/WordCount.class: WordCount.java
	mkdir -p build
	javac -cp /usr/lib/hadoop/*:/usr/lib/hadoop-mapreduce/* WordCount.java -d build -Xlint

clean:
	rm -rf build wordcount.jar

data:
	hadoop fs -rm -f -r /user/cloudera/wordcount/input
	hadoop fs -mkdir /user/cloudera/wordcount
	hadoop fs -mkdir /user/cloudera/wordcount/input
	echo "Hadoop is an elephant" > file0
	echo "Hadoop is as yellow as can be" > file1
	echo "Oh what a yellow fellow is Hadoop" > file2
	hadoop fs -put file* /user/cloudera/wordcount/input
	rm file*

poetry:
	hadoop fs -rm -f -r /user/cloudera/wordcount/input
	hadoop fs -mkdir /user/cloudera/wordcount/input
	echo -e "Hadoop is the Elephant King! \\nA yellow and elegant thing.\\nHe never forgets\\nUseful data, or lets\\nAn extraneous element cling! "> HadoopPoem0.txt
	echo -e "A wonderful king is Hadoop.\\nThe elephant plays well with Sqoop.\\nBut what helps him to thrive\\nAre Impala, and Hive,\\nAnd HDFS in the group." > HadoopPoem1.txt
	echo -e "Hadoop is an elegant fellow.\\nAn elephant gentle and mellow.\\nHe never gets mad,\\nOr does anything bad,\\nBecause, at his core, he is yellow." > HadoopPoem2.txt
	hadoop fs -put HadoopP* /user/cloudera/wordcount/input
	rm HadoopPoem*

showResult:
	hadoop fs -cat /user/cloudera/wordcount/output/*
	
stopwords:
	hadoop fs -rm -f /user/cloudera/wordcount/stop_words.text
	echo -e "a\\nan\\nand\\nbut\\nis\\nor\\nthe\\nto\\n.\\n," >stop_words.text
	hadoop fs -put stop_words.text /user/cloudera/wordcount/


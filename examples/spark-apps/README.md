# Spark Applications

## spark-sql Apps
table population:

```
val person = Seq(
    (0, "Bill Chambers", 0, Seq(100)),
    (1, "Matei Zaharia", 1, Seq(500, 250, 100)),
    (2, "Michael Armbrust", 1, Seq(250, 100))).toDF("id", "name", "graduate_program", "spark_status")
val graduateProgram = Seq(
    (0, "Masters", "School of Information", "UC Berkeley"),
    (2, "Masters", "EECS", "UC Berkeley"),
    (1, "Ph.D.", "EECS", "UC Berkeley")).toDF("id", "degree", "department", "school")
val sparkStatus = Seq(
    (500, "Vice President"),
    (250, "PMC Member"),
    (100, "Contributor")).toDF("id", "status")
person.write.format("parquet").saveAsTable("person")
graduateProgram.write.format("parquet").saveAsTable("graduate_program")
sparkStatus.write.format("parquet").saveAsTable("spark_status")
```

```
spark-sql --conf spark.sql.autoBroadcastJoinThreshold=-1 --conf spark.sql.codegen.wholeStage=false
```

join:

```
select p.id, p.name, gp.school from person p join graduate_program gp on p.graduate_program = gp.id;
```

scalar subquery:

```
select p.id, p.name, gp.school, (select count(1) from person) total from person p join graduate_program gp on p.graduate_program = gp.id;
```

correlated subquery:

```
select p.id, p.name, gp.school, (select count(1) from graduate_program gp2 where gp2.school=gp.school) alumni from person p join graduate_program gp on p.graduate_program = gp.id;
```

## Standalone Apps
Spark project that uses Maven for building.  The app simply counts the number of lines in
a text file.

To build a JAR:

    mvn clean package

To run locally with Spark installed:

    spark-submit --master local target/spark-apps-0.1.0-jar-with-dependencies.jar <input file>

To run a REPL that can reference the objects and classes defined in this project:

    spark-shell --jars target/spark-apps-0.1.0-jar-with-dependencies.jar --master local

The `--master local` argument means that the application will run in a single local process. If the
cluster is running YARN, you can replace it with `--master yarn`.

To pass configuration options on the command line, use the `--conf` option, e.g.
`--conf spark.serializer=org.apache.spark.serializer.KryoSerializer`.

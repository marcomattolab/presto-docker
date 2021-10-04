
See => https://prestodb.io/docs/current/installation/deployment.html


>> docker build --build-arg PRESTO_VERSION="0.262" . -t prestodb:latest
>> docker run --name presto prestodb:latest


Use the Presto CLI to connect to Presto:
>> docker exec -it presto presto

We can now execute a query against the tpch catalog:
SELECT
   l.returnflag,
   l.linestatus,
   sum(l.quantity)                                       AS sum_qty,
   sum(l.extendedprice)                                  AS sum_base_price,
   sum(l.extendedprice * (1 - l.discount))               AS sum_disc_price,
   sum(l.extendedprice * (1 - l.discount) * (1 + l.tax)) AS sum_charge,
   avg(l.quantity)                                       AS avg_qty,
   avg(l.extendedprice)                                  AS avg_price,
   avg(l.discount)                                       AS avg_disc,
   count(*)                                              AS count_order
 FROM
   tpch.sf1.lineitem AS l
 WHERE
   l.shipdate <= DATE '1998-12-01' - INTERVAL '90' DAY
 GROUP BY
   l.returnflag,
   l.linestatus
 ORDER BY
   l.returnflag,
   l.linestatus;



Others:
https://github.com/johannestang/bigdata_stack
https://docs.starburst.io/312-e/docker.html
https://raw.githubusercontent.com/johannestang/bigdata_stack/master/docker-compose.yml
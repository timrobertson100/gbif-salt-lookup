# Populates an HBase table with salted keys.

Build the project: `mvn clean package`

Example usage from a gateway:

Create the target tables:

```
create 'tim_salted_occ_lookup',
  {NAME => 'o', VERSIONS => 1, COMPRESSION => 'SNAPPY', DATA_BLOCK_ENCODING => 'FAST_DIFF', BLOOMFILTER => 'ROW'},
{SPLITS => [
    '01','02','03','04','05','06','07','08','09','10',
    '11','12','13','14','15','16','17','18','19','20',
    '21','22','23','24','25','26','27','28','29','30',
    '31','32','33','34','35','36','37','38','39','40',
    '41','42','43','44','45','46','47','48','49','50',
    '51','52','53','54','55','56','57','58','59','60',
    '61','62','63','64','65','66','67','68','69','70',
    '71','72','73','74','75','76','77','78','79','80',
    '81','82','83','84','85','86','87','88','89','90',
    '91','92','93','94','95','96','97','98','99'
  ]}
```

Execute on a CDH managed gateway:

```
sudo -u hdfs  HADOOP_CLASSPATH=`${HBASE_HOME}/bin/hbase classpath` \
  hadoop jar ./salt-lookup-keys-1.0-SNAPSHOT.jar org.gbif.fixup.occurrence.SaltOccurrenceKeyDriver \
  -zk c4master1-vh.gbif.org,c4master2-vh.gbif.org,c4master3-vh.gbif.org \
  -src uat_occurrence_lookup \
  -target tim_salted_occ_lookup \
  -tmpPath /tmp/saltLookupTmp
```


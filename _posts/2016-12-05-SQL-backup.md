---
layout:     post
title:      SQL Backup get the full details about the table and time 
category:   [SQL] 
tags:       [SQL]
---

SQL Backup

{% highlight SQL %}
-- pgSQL
-- Get the table full description and columns 

SELECT DISTINCT
    a.attnum as num,
    a.attname as name,
    format_type(a.atttypid, a.atttypmod) as typ,
    a.attnotnull as notnull, 
    com.description as comment,
    coalesce(i.indisprimary,false) as primary_key,
    def.adsrc as default
FROM pg_attribute a 
JOIN pg_class pgc ON pgc.oid = a.attrelid
LEFT JOIN pg_index i ON 
    (pgc.oid = i.indrelid AND i.indkey[0] = a.attnum)
LEFT JOIN pg_description com on 
    (pgc.oid = com.objoid AND a.attnum = com.objsubid)
LEFT JOIN pg_attrdef def ON 
    (a.attrelid = def.adrelid AND a.attnum = def.adnum)
WHERE a.attnum > 0 AND pgc.oid = a.attrelid
AND pg_table_is_visible(pgc.oid)
AND NOT a.attisdropped
AND pgc.relname = 'bvd_etl_log'  -- Your table name here
ORDER BY a.attnum;

-- TIME
select cus_prov_id, amount, yoy, mom, ((the_year||the_month||'01')::date + interval'1 month' - interval'1 day')::date as data_date from ebd_stgcustoms_stat_prov_e where the_year||the_month < '201512' and the_year||the_month >= '201212'


-- ORACLE
select * from ebd_signal_score_result where update_date = to_date('2016/11/26', 'YYYY/MM/DD')
{% endhighlight %}
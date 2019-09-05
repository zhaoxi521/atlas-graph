<template>
  <div ref="wrapper" style="width: 100%; height: 100%">
    <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg" version="1.1"></svg>
  </div>
</template>

<script>
import * as d3 from 'd3'
import * as dagreD3 from 'dagre-d3'

const respond = {
  'baseEntityGuid': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
  'lineageDirection': 'BOTH',
  'lineageDepth': 3,
  'guidEntityMap': {
    'bbeabdf9-d0d4-4427-8c16-ebf346b4b0da': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em_union1@primary:1566368140000:db_lineage.em_union2@primary:1566368194000->:INSERT_OVERWRITE:db_lineage.em_part3@primary:1566369280000',
        'name': 'insert overwrite table em_part3 select * from ( select * from em_union2 where sex=\'man\')t1union all select * from (select * from em_union1 where age>=24) t2union all select * from em1'
      },
      'guid': 'bbeabdf9-d0d4-4427-8c16-ebf346b4b0da',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em_part3 select * from ( select * from em_union2 where sex=\'man\')t1union all select * from (select * from em_union1 where age>=24) t2union all select * from em1',
      'classificationNames': []
    },
    '9c1916f7-3843-4e11-a5a4-181e57a04d01': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566368451000,
        'qualifiedName': 'db_lineage.em_leftouter_join@primary',
        'name': 'em_leftouter_join'
      },
      'guid': '9c1916f7-3843-4e11-a5a4-181e57a04d01',
      'status': 'ACTIVE',
      'displayText': 'em_leftouter_join',
      'classificationNames': []
    },
    '08828890-bd71-433b-8298-c096c0e602ae': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566369280000,
        'qualifiedName': 'db_lineage.em_part3@primary',
        'name': 'em_part3'
      },
      'guid': '08828890-bd71-433b-8298-c096c0e602ae',
      'status': 'ACTIVE',
      'displayText': 'em_part3',
      'classificationNames': []
    },
    'ef549d6f-12d5-4919-bb70-d43f58a721d2': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566368496000,
        'qualifiedName': 'db_lineage.em_part1@primary',
        'name': 'em_part1'
      },
      'guid': 'ef549d6f-12d5-4919-bb70-d43f58a721d2',
      'status': 'ACTIVE',
      'displayText': 'em_part1',
      'classificationNames': []
    },
    'bd3373a7-aaed-482a-a7d7-b47e265f4010': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566369086000,
        'qualifiedName': 'db_lineage.em_part2@primary',
        'name': 'em_part2'
      },
      'guid': 'bd3373a7-aaed-482a-a7d7-b47e265f4010',
      'status': 'ACTIVE',
      'displayText': 'em_part2',
      'classificationNames': []
    },
    'c561680f-412e-4a49-ad83-f5de5c8ba237': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'db_lineage.em_leftouter_join@primary:1566368451000',
        'name': 'create table em_leftouter_join as select e1.id,e1.name,e1.age,e2.sex from em1 e1 left outer join em2 e2 on (e1.age=e2.age)'
      },
      'guid': 'c561680f-412e-4a49-ad83-f5de5c8ba237',
      'status': 'ACTIVE',
      'displayText': 'create table em_leftouter_join as select e1.id,e1.name,e1.age,e2.sex from em1 e1 left outer join em2 e2 on (e1.age=e2.age)',
      'classificationNames': []
    },
    '67ad547f-fa4b-445b-917e-cefd719b9b79': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566368194000,
        'qualifiedName': 'db_lineage.em_union2@primary',
        'name': 'em_union2'
      },
      'guid': '67ad547f-fa4b-445b-917e-cefd719b9b79',
      'status': 'ACTIVE',
      'displayText': 'em_union2',
      'classificationNames': []
    },
    'eada0402-25c7-4b57-a0c9-0b7f8f5f2b51': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566367795000,
        'qualifiedName': 'db_lineage.em5@primary',
        'name': 'em5'
      },
      'guid': 'eada0402-25c7-4b57-a0c9-0b7f8f5f2b51',
      'status': 'ACTIVE',
      'displayText': 'em5',
      'classificationNames': []
    },
    '7a234b9c-e7f5-44dc-9704-dee2fe81250a': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em2@primary:1566274814000->:INSERT_OVERWRITE:db_lineage.em3@primary:1566274875000',
        'name': 'insert overwrite table em3 select * from em1 union all select * from em2'
      },
      'guid': '7a234b9c-e7f5-44dc-9704-dee2fe81250a',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em3 select * from em1 union all select * from em2',
      'classificationNames': []
    },
    'a3b80efe-c37f-4387-8ca1-e7867bc29299': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em3@primary:1566274875000:db_lineage.em6@primary:1566367883000:db_lineage.em8@primary:1566368012000:db_lineage.em_union1@primary:1566368140000->:INSERT_OVERWRITE:db_lineage.em_union3@primary:1566368357000',
        'name': 'insert overwrite table em_union3 select * from em_union1 union all select * from em6 union all select * from em3 union all select * from em1 union all select * from em8'
      },
      'guid': 'a3b80efe-c37f-4387-8ca1-e7867bc29299',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em_union3 select * from em_union1 union all select * from em6 union all select * from em3 union all select * from em1 union all select * from em8',
      'classificationNames': []
    },
    '2d3a8fb8-ab5e-434c-bda4-7edd9e4d1895': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566367883000,
        'qualifiedName': 'db_lineage.em6@primary',
        'name': 'em6'
      },
      'guid': '2d3a8fb8-ab5e-434c-bda4-7edd9e4d1895',
      'status': 'ACTIVE',
      'displayText': 'em6',
      'classificationNames': []
    },
    '6d419c97-abc2-475f-8e56-6c6a0ab92af8': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566368012000,
        'qualifiedName': 'db_lineage.em8@primary',
        'name': 'em8'
      },
      'guid': '6d419c97-abc2-475f-8e56-6c6a0ab92af8',
      'status': 'ACTIVE',
      'displayText': 'em8',
      'classificationNames': []
    },
    '8dfa1965-315f-4216-870c-eae8b715f569': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em3@primary:1566274875000:db_lineage.em6@primary:1566367883000:db_lineage.em_union1@primary:1566368140000->:INSERT_OVERWRITE:db_lineage.em_union2@primary:1566368194000',
        'name': 'insert overwrite table em_union2 select * from em_union1 union all select * from em6 union all select * from em3 union all select * from em1'
      },
      'guid': '8dfa1965-315f-4216-870c-eae8b715f569',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em_union2 select * from em_union1 union all select * from em6 union all select * from em3 union all select * from em1',
      'classificationNames': []
    },
    '194ca1d0-9e72-4e0f-9b9d-1d9c91002006': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'LOAD->:db_lineage.em1@primary:1566273191000',
        'name': 'load data local inpath /root/em1.txt into table em1'
      },
      'guid': '194ca1d0-9e72-4e0f-9b9d-1d9c91002006',
      'status': 'ACTIVE',
      'displayText': 'load data local inpath /root/em1.txt into table em1',
      'classificationNames': []
    },
    '32fd7487-d7c2-439f-951d-ed9c713c2a24': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566274875000,
        'qualifiedName': 'db_lineage.em3@primary',
        'name': 'em3'
      },
      'guid': '32fd7487-d7c2-439f-951d-ed9c713c2a24',
      'status': 'ACTIVE',
      'displayText': 'em3',
      'classificationNames': []
    },
    '7d69d8b4-4bce-42db-98ff-1aa8a10396f6': {
      'typeName': 'hdfs_path',
      'attributes': {
        'createTime': 0,
        'qualifiedName': 'hdfs://node101.gla.net.cn:8020/user/hive/warehouse/db_lineage.db/em1@primary',
        'name': '/user/hive/warehouse/db_lineage.db/em1'
      },
      'guid': '7d69d8b4-4bce-42db-98ff-1aa8a10396f6',
      'status': 'ACTIVE',
      'displayText': '/user/hive/warehouse/db_lineage.db/em1',
      'classificationNames': []
    },
    '49d958a2-1aef-49ff-9049-42fabeca1dc7': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566273191000,
        'qualifiedName': 'db_lineage.em1@primary',
        'name': 'em1'
      },
      'guid': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'status': 'ACTIVE',
      'displayText': 'em1',
      'classificationNames': []
    },
    '680c26c2-e177-425a-b4dd-f607c6f0efdb': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566367946000,
        'qualifiedName': 'db_lineage.em7@primary',
        'name': 'em7'
      },
      'guid': '680c26c2-e177-425a-b4dd-f607c6f0efdb',
      'status': 'ACTIVE',
      'displayText': 'em7',
      'classificationNames': []
    },
    '3f3364ef-a99c-4109-a844-d985b52e82eb': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em2@primary:1566274814000:db_lineage.em3@primary:1566274875000->:INSERT_OVERWRITE:db_lineage.em6@primary:1566367883000',
        'name': 'insert overwrite table em6 select * from em1 union all select * from em2 union all select * from em3'
      },
      'guid': '3f3364ef-a99c-4109-a844-d985b52e82eb',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em6 select * from em1 union all select * from em2 union all select * from em3',
      'classificationNames': []
    },
    'cb51802d-ea7f-40d2-888f-40ce2ab984fa': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em2@primary:1566274814000:db_lineage.em3@primary:1566274875000->:INSERT_OVERWRITE:db_lineage.em5@primary:1566367795000',
        'name': 'insert overwrite table em5 select * from em2 union all select * from em3'
      },
      'guid': 'cb51802d-ea7f-40d2-888f-40ce2ab984fa',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em5 select * from em2 union all select * from em3',
      'classificationNames': []
    },
    '1e5ebdea-525a-45b0-91ab-fcc68b0c5b5c': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em_union1@primary:1566368140000->:INSERT_OVERWRITE:db_lineage.em_part2@primary:1566369086000',
        'name': 'insert overwrite table em_part2select * from (select * from em_union1 where age>=24) t1union all select * from em1'
      },
      'guid': '1e5ebdea-525a-45b0-91ab-fcc68b0c5b5c',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em_part2select * from (select * from em_union1 where age>=24) t1union all select * from em1',
      'classificationNames': []
    },
    '79eb3825-f38b-4571-b1db-fc487826284e': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em2@primary:1566274814000:db_lineage.em3@primary:1566274875000:db_lineage.em5@primary:1566367795000:db_lineage.em6@primary:1566367883000->:INSERT_OVERWRITE:db_lineage.em7@primary:1566367946000',
        'name': 'insert overwrite table em7 select * from em1 union all select * from em2 union all select * from em3 union all select * from em5 union all select * from em6'
      },
      'guid': '79eb3825-f38b-4571-b1db-fc487826284e',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em7 select * from em1 union all select * from em2 union all select * from em3 union all select * from em5 union all select * from em6',
      'classificationNames': []
    },
    'b5491950-8507-46fa-a1cd-b8c7e9d17abd': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566368357000,
        'qualifiedName': 'db_lineage.em_union3@primary',
        'name': 'em_union3'
      },
      'guid': 'b5491950-8507-46fa-a1cd-b8c7e9d17abd',
      'status': 'ACTIVE',
      'displayText': 'em_union3',
      'classificationNames': []
    },
    '3d55b9da-e8c6-4fab-b8f3-0ffed98f9977': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em_union3@primary:1566368357000->:INSERT_OVERWRITE:db_lineage.em_part1@primary:1566368496000',
        'name': 'insert overwrite table em_part1 select * from em_union3 where age<25'
      },
      'guid': '3d55b9da-e8c6-4fab-b8f3-0ffed98f9977',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em_part1 select * from em_union3 where age<25',
      'classificationNames': []
    },
    'fd979082-0b4c-4437-8a39-5ad9e506cfac': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em2@primary:1566274814000:db_lineage.em5@primary:1566367795000:db_lineage.em6@primary:1566367883000:db_lineage.em7@primary:1566367946000->:INSERT_OVERWRITE:db_lineage.em8@primary:1566368012000',
        'name': 'insert overwrite table em8 select * from em1 union all select * from em2 union all select * from em6 union all select * from em5 union all select * from em7'
      },
      'guid': 'fd979082-0b4c-4437-8a39-5ad9e506cfac',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em8 select * from em1 union all select * from em2 union all select * from em6 union all select * from em5 union all select * from em7',
      'classificationNames': []
    },
    '57782561-42cf-48a2-bb4e-628dc6227853': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566367754000,
        'qualifiedName': 'db_lineage.em4@primary',
        'name': 'em4'
      },
      'guid': '57782561-42cf-48a2-bb4e-628dc6227853',
      'status': 'ACTIVE',
      'displayText': 'em4',
      'classificationNames': []
    },
    'c3433135-a655-49e2-87f0-15ed5f4c9637': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em6@primary:1566367883000->:INSERT_OVERWRITE:db_lineage.em_union1@primary:1566368140000',
        'name': 'insert overwrite table em_union1 select * from em1 union all select * from em6'
      },
      'guid': 'c3433135-a655-49e2-87f0-15ed5f4c9637',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em_union1 select * from em1 union all select * from em6',
      'classificationNames': []
    },
    'e4e24102-12f0-4cb4-8394-57775eb874cf': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'QUERY:db_lineage.em1@primary:1566273191000:db_lineage.em3@primary:1566274875000->:INSERT_OVERWRITE:db_lineage.em4@primary:1566367754000',
        'name': 'insert overwrite table em4 select * from em1 union all select * from em3'
      },
      'guid': 'e4e24102-12f0-4cb4-8394-57775eb874cf',
      'status': 'ACTIVE',
      'displayText': 'insert overwrite table em4 select * from em1 union all select * from em3',
      'classificationNames': []
    },
    'a209e9b5-43ef-44d6-9508-dc75c43c80a9': {
      'typeName': 'hive_process',
      'attributes': {
        'qualifiedName': 'db_lineage.em1@primary:1566273191000',
        'name': 'create external table em1(id int ,name string,age int,sex string) row formatdelimited fields terminated by \',\''
      },
      'guid': 'a209e9b5-43ef-44d6-9508-dc75c43c80a9',
      'status': 'ACTIVE',
      'displayText': 'create external table em1(id int ,name string,age int,sex string) row formatdelimited fields terminated by \',\'',
      'classificationNames': []
    },
    'efbeea31-a1cb-4120-8d4e-dc512398c50c': {
      'typeName': 'hive_table',
      'attributes': {
        'owner': 'root',
        'createTime': 1566368140000,
        'qualifiedName': 'db_lineage.em_union1@primary',
        'name': 'em_union1'
      },
      'guid': 'efbeea31-a1cb-4120-8d4e-dc512398c50c',
      'status': 'ACTIVE',
      'displayText': 'em_union1',
      'classificationNames': []
    }
  },
  'relations': [
    {
      'fromEntityId': 'cb51802d-ea7f-40d2-888f-40ce2ab984fa',
      'toEntityId': 'eada0402-25c7-4b57-a0c9-0b7f8f5f2b51'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': '1e5ebdea-525a-45b0-91ab-fcc68b0c5b5c'
    },
    {
      'fromEntityId': 'a3b80efe-c37f-4387-8ca1-e7867bc29299',
      'toEntityId': 'b5491950-8507-46fa-a1cd-b8c7e9d17abd'
    },
    {
      'fromEntityId': '2d3a8fb8-ab5e-434c-bda4-7edd9e4d1895',
      'toEntityId': 'a3b80efe-c37f-4387-8ca1-e7867bc29299'
    },
    {
      'fromEntityId': '6d419c97-abc2-475f-8e56-6c6a0ab92af8',
      'toEntityId': 'a3b80efe-c37f-4387-8ca1-e7867bc29299'
    },
    {
      'fromEntityId': '2d3a8fb8-ab5e-434c-bda4-7edd9e4d1895',
      'toEntityId': 'fd979082-0b4c-4437-8a39-5ad9e506cfac'
    },
    {
      'fromEntityId': '2d3a8fb8-ab5e-434c-bda4-7edd9e4d1895',
      'toEntityId': '8dfa1965-315f-4216-870c-eae8b715f569'
    },
    {
      'fromEntityId': '2d3a8fb8-ab5e-434c-bda4-7edd9e4d1895',
      'toEntityId': '79eb3825-f38b-4571-b1db-fc487826284e'
    },
    {
      'fromEntityId': 'fd979082-0b4c-4437-8a39-5ad9e506cfac',
      'toEntityId': '6d419c97-abc2-475f-8e56-6c6a0ab92af8'
    },
    {
      'fromEntityId': '67ad547f-fa4b-445b-917e-cefd719b9b79',
      'toEntityId': 'bbeabdf9-d0d4-4427-8c16-ebf346b4b0da'
    },
    {
      'fromEntityId': '32fd7487-d7c2-439f-951d-ed9c713c2a24',
      'toEntityId': 'a3b80efe-c37f-4387-8ca1-e7867bc29299'
    },
    {
      'fromEntityId': '32fd7487-d7c2-439f-951d-ed9c713c2a24',
      'toEntityId': '8dfa1965-315f-4216-870c-eae8b715f569'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': '3f3364ef-a99c-4109-a844-d985b52e82eb'
    },
    {
      'fromEntityId': 'eada0402-25c7-4b57-a0c9-0b7f8f5f2b51',
      'toEntityId': '79eb3825-f38b-4571-b1db-fc487826284e'
    },
    {
      'fromEntityId': '3d55b9da-e8c6-4fab-b8f3-0ffed98f9977',
      'toEntityId': 'ef549d6f-12d5-4919-bb70-d43f58a721d2'
    },
    {
      'fromEntityId': '32fd7487-d7c2-439f-951d-ed9c713c2a24',
      'toEntityId': '79eb3825-f38b-4571-b1db-fc487826284e'
    },
    {
      'fromEntityId': 'efbeea31-a1cb-4120-8d4e-dc512398c50c',
      'toEntityId': '8dfa1965-315f-4216-870c-eae8b715f569'
    },
    {
      'fromEntityId': 'eada0402-25c7-4b57-a0c9-0b7f8f5f2b51',
      'toEntityId': 'fd979082-0b4c-4437-8a39-5ad9e506cfac'
    },
    {
      'fromEntityId': 'efbeea31-a1cb-4120-8d4e-dc512398c50c',
      'toEntityId': 'a3b80efe-c37f-4387-8ca1-e7867bc29299'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': 'c3433135-a655-49e2-87f0-15ed5f4c9637'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': '79eb3825-f38b-4571-b1db-fc487826284e'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': 'a3b80efe-c37f-4387-8ca1-e7867bc29299'
    },
    {
      'fromEntityId': 'efbeea31-a1cb-4120-8d4e-dc512398c50c',
      'toEntityId': '1e5ebdea-525a-45b0-91ab-fcc68b0c5b5c'
    },
    {
      'fromEntityId': 'bbeabdf9-d0d4-4427-8c16-ebf346b4b0da',
      'toEntityId': '08828890-bd71-433b-8298-c096c0e602ae'
    },
    {
      'fromEntityId': 'c561680f-412e-4a49-ad83-f5de5c8ba237',
      'toEntityId': '9c1916f7-3843-4e11-a5a4-181e57a04d01'
    },
    {
      'fromEntityId': 'a209e9b5-43ef-44d6-9508-dc75c43c80a9',
      'toEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7'
    },
    {
      'fromEntityId': '3f3364ef-a99c-4109-a844-d985b52e82eb',
      'toEntityId': '2d3a8fb8-ab5e-434c-bda4-7edd9e4d1895'
    },
    {
      'fromEntityId': '7d69d8b4-4bce-42db-98ff-1aa8a10396f6',
      'toEntityId': 'a209e9b5-43ef-44d6-9508-dc75c43c80a9'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': 'c561680f-412e-4a49-ad83-f5de5c8ba237'
    },
    {
      'fromEntityId': '1e5ebdea-525a-45b0-91ab-fcc68b0c5b5c',
      'toEntityId': 'bd3373a7-aaed-482a-a7d7-b47e265f4010'
    },
    {
      'fromEntityId': 'c3433135-a655-49e2-87f0-15ed5f4c9637',
      'toEntityId': 'efbeea31-a1cb-4120-8d4e-dc512398c50c'
    },
    {
      'fromEntityId': '680c26c2-e177-425a-b4dd-f607c6f0efdb',
      'toEntityId': 'fd979082-0b4c-4437-8a39-5ad9e506cfac'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': 'bbeabdf9-d0d4-4427-8c16-ebf346b4b0da'
    },
    {
      'fromEntityId': '8dfa1965-315f-4216-870c-eae8b715f569',
      'toEntityId': '67ad547f-fa4b-445b-917e-cefd719b9b79'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': 'e4e24102-12f0-4cb4-8394-57775eb874cf'
    },
    {
      'fromEntityId': '79eb3825-f38b-4571-b1db-fc487826284e',
      'toEntityId': '680c26c2-e177-425a-b4dd-f607c6f0efdb'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': 'fd979082-0b4c-4437-8a39-5ad9e506cfac'
    },
    {
      'fromEntityId': 'efbeea31-a1cb-4120-8d4e-dc512398c50c',
      'toEntityId': 'bbeabdf9-d0d4-4427-8c16-ebf346b4b0da'
    },
    {
      'fromEntityId': '7a234b9c-e7f5-44dc-9704-dee2fe81250a',
      'toEntityId': '32fd7487-d7c2-439f-951d-ed9c713c2a24'
    },
    {
      'fromEntityId': '32fd7487-d7c2-439f-951d-ed9c713c2a24',
      'toEntityId': 'cb51802d-ea7f-40d2-888f-40ce2ab984fa'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': '8dfa1965-315f-4216-870c-eae8b715f569'
    },
    {
      'fromEntityId': '32fd7487-d7c2-439f-951d-ed9c713c2a24',
      'toEntityId': 'e4e24102-12f0-4cb4-8394-57775eb874cf'
    },
    {
      'fromEntityId': 'b5491950-8507-46fa-a1cd-b8c7e9d17abd',
      'toEntityId': '3d55b9da-e8c6-4fab-b8f3-0ffed98f9977'
    },
    {
      'fromEntityId': '2d3a8fb8-ab5e-434c-bda4-7edd9e4d1895',
      'toEntityId': 'c3433135-a655-49e2-87f0-15ed5f4c9637'
    },
    {
      'fromEntityId': '194ca1d0-9e72-4e0f-9b9d-1d9c91002006',
      'toEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7'
    },
    {
      'fromEntityId': '49d958a2-1aef-49ff-9049-42fabeca1dc7',
      'toEntityId': '7a234b9c-e7f5-44dc-9704-dee2fe81250a'
    },
    {
      'fromEntityId': 'e4e24102-12f0-4cb4-8394-57775eb874cf',
      'toEntityId': '57782561-42cf-48a2-bb4e-628dc6227853'
    },
    {
      'fromEntityId': '32fd7487-d7c2-439f-951d-ed9c713c2a24',
      'toEntityId': '3f3364ef-a99c-4109-a844-d985b52e82eb'
    }
  ]
}
const guid = '49d958a2-1aef-49ff-9049-42fabeca1dc7'

export default {
  name: 'Lineage',
  mounted () {
    // 获取数据，渲染视图
    this.getData().renderGraph()
  },
  methods: {
    // 获取数据数据
    getData () {
      // 当前GUID
      this.guid = guid
      // 所有数据
      this.lineageData = respond
      // 节点关系
      this.relationshipMap = this.crateLineageRelationshipHashMap(respond.relations)
      // 节点数据
      this.nodeMap = this.crateGuidEntityHashMap(respond.guidEntityMap)
      // 返回自身
      return this
    },
    // 初始化视图
    initGraph () {
      // 创建视图
      this.g = new dagreD3.graphlib.Graph().setGraph({
        nodesep: 50,
        ranksep: 90,
        rankdir: 'LR',
        marginx: 20,
        marginy: 20,
        transition: function (selection) {
          return selection.transition().duration(500)
        }
      }).setDefaultEdgeLabel(function () {
        return {}
      })
      return this
    },
    // 创建视图
    createGraph () {
      const that = this
      // 设置一个图片存储对象
      const imageObject = {}
      // 设置每个节点
      this.g.nodes().forEach((v) => {
        const node = this.g.node(v)
        node && (node.rx = node.ry = 5)
      })
      // 创建渲染
      // eslint-disable-next-line new-cap
      const render = new dagreD3.render()

      // 重新定义三角
      render.arrows().arrowPoint = (parent, id, edge, type) => {
        // 一个标志位，用于样式变化
        parent.attr('to', edge.to)
        // 设置其他格式
        let marker = parent.append('marker')
          .attr('id', id)
          .attr('viewBox', '0 0 10 10')
          .attr('refX', 8)
          .attr('refY', 5)
          .attr('markerUnits', 'strokeWidth')
          .attr('markerWidth', 4)
          .attr('markerHeight', 4)
          .attr('orient', 'auto')
        let path = marker.append('path')
          .attr('d', 'M 0 0 L 10 5 L 0 10 z')
          .style('fill', edge.styleObj.stroke)
        dagreD3.util.applyStyle(path, edge[type + 'Style'])
      }

      // 重新定义节点图形
      render.shapes().img = (parent, bbox, node) => {
        // 是否是当前查看节点
        const currentNode = node.guid === this.guid
        // 设置图形（圆形）
        const shapeSvg = parent.append('circle')
          .attr('fill', 'url(#img_' + node.guid + ')')
          .attr('r', '24px')
          .attr('data-stroke', node.guid)
          .attr('stroke-width', '2px')
          .attr('class', 'nodeImage ' + (currentNode ? 'currentNode' : 'node'))
        // 当前查看节点，高亮
        currentNode && shapeSvg.attr('stroke', '#fb4200')
        // 添加defs
        parent.insert('defs')
          .append('pattern')
          .attr('x', '0%')
          .attr('y', '0%')
          .attr('patternUnits', 'objectBoundingBox')
          .attr('id', 'img_' + node.guid)
          .attr('width', '100%')
          .attr('height', '100%')
          .append('image')
          .attr('href', () => {
            if (node) {
              const imagePath = `./img/${node.typeName}.png`
              this.getUrlBase64(imagePath, 'png', (data) => {
                if (!imageObject[node.typeName]) {
                  imageObject[node.typeName] = data
                }
                return parent.select('image').attr('xlink:href', imageObject[node.typeName])
              })
            }
          })
          .attr('x', '4')
          .attr('y', currentNode ? '3' : '4')
          .attr('width', '40')
          .attr('height', '40')
        // 节点交叉处理
        node.intersect = function (point) {
          return dagreD3.intersect.circle(node, currentNode ? 24 : 21, point)
        }
        return shapeSvg
      }

      // 获取容器
      const svg = d3.select('svg')
      const svgGroup = svg.append('g')

      // 给容器设置缩放
      const zoom = d3.zoom().on('zoom', function () {
        svgGroup.attr('transform', d3.event.transform)
      })

      // 获取当前宽和高
      const w = that.$refs.wrapper.clientWidth
      const h = that.$refs.wrapper.clientHeight
      svg.call(zoom)
        // 设置双击不能缩放
        .on('dblclick.zoom', null)
        // 设置容器变化，图表变化
        .attr('preserveAspectRatio', 'xMinYMin meet')
        .attr('viewBox', '0 0 ' + w + ' ' + h)
        .attr('enable-background', 'new 0 0 ' + w + ' ' + h)

      // 渲染图表
      render(svgGroup, this.g)

      // 设置中心
      // 获取图形的宽和高
      const graphWidth = this.g.graph().width
      const graphHeight = this.g.graph().height
      // 比较出缩放比例
      let initialScale = Math.min(Math.min(w / graphWidth, h / graphHeight), 1) * 0.9
      // 移动的距离
      const translateX = (w - graphWidth * initialScale) / 2
      const translateY = (h - graphHeight * initialScale) / 2
      // 设置
      svg.call(zoom.transform, d3.zoomIdentity.translate(translateX, translateY).scale(initialScale))

      // 设置节点label位置
      svgGroup.selectAll('g.nodes g.label').attr('transform', 'translate(2,-35)')

      // 设置放大倍数
      const scale = 'scale(1.3)'
      // 拖拽的状态
      let dragging = false
      // 设置hover事件
      svgGroup.selectAll('g.nodes g.node circle')
        .on('mouseenter', function (d) {
          // 正在拖拽
          if (dragging) return
          // 设置放大效果
          // 获取d3DOM实例
          const current = d3.select(this.parentNode)
          current.attr('transform', `${current.attr('transform')}${scale}`)
          // 获取连接的数据节点
          const predecessors = that.g.predecessors(d) // 前
          const successors = that.g.successors(d) // 后
          // 设置对应节点高亮
          const nodesToHighlight = predecessors.concat(successors, d)
          that.g.nodes().forEach((v) => {
            const node = that.g.node(v)
            if (nodesToHighlight.includes(v)) {
              node.elem.style.opacity = 1
            } else {
              node.elem.style.opacity = 0.2
            }
          })
          // 设置对应连接线高亮
          const pathsToHighlight = predecessors.concat(successors)
          Object.keys(that.g._edgeLabels).forEach(t => {
          // 每个edge数据
            const val = that.g._edgeLabels[t]
            val.elem.style.opacity = 0.2
            pathsToHighlight.forEach(m => {
              if (t.includes(m) && t.includes(d)) {
                val.elem.style.opacity = 1
              }
            })
          })
        })
        .on('mouseleave', function () {
          // 正在拖拽
          if (dragging) return
          // 获取d3DOM实例
          const current = d3.select(this.parentNode)
          current.attr('transform', `${current.attr('transform').replace(scale, '')}`)
          // 设置所有节点高亮
          that.g.nodes().forEach((v) => {
            that.g.node(v).elem.style.opacity = 1
          })
          // 设置所有连接线高亮
          Object.values(that.g._edgeLabels).forEach(t => {
            t.elem.style.opacity = 1
          })
        })
        .on('click', function (d) {
          if (d3.event.defaultPrevented) return
          alert(d)
        })
        .call(d3.drag()
          .on('start', dragStarted)
          .on('drag', dragged)
          .on('end', dragEnd))

      // 拖拽事件
      function dragStarted () {
        // 拖拽开始
        dragging = true
        d3.event.sourceEvent.stopPropagation()
      }

      function dragged (d) {
        // =====================================
        // 修改节点位置
        // 获取当前的node的选择器实例
        const nodeSelection = d3.select(this.parentNode)
        // 获取当前的node
        const node = that.g.node(d)
        // 更新后的位置
        node.x += d3.event.x
        node.y += d3.event.y
        // 更新节点
        nodeSelection.attr('transform', `translate(${node.x},${node.y})${scale}`)
        // =====================================
        // 修改线的位置
        that.g.edges().forEach(t => {
          if (t.v === d || t.w === d) {
            // 得到所有的连线数据
            const edge = that.g.edge(t.v, t.w)
            // 更新点位置
            edge.points.forEach(p => {
              p.x = p.x + d3.event.x
              p.y = p.y + d3.event.y
            })
            const points = edge.points.slice(1, edge.points.length - 1)
            points.unshift(intersectRect(that.g.node(t.v), edge.points[0]))
            points.push(intersectRect(that.g.node(t.w), edge.points[edge.points.length - 1]))
            // 更新线的位置
            const selection = d3.select(edge.elem).select('path')
            selection.attr('d', d3.line().x(m => m.x).y(m => m.y).curve(d3.curveBasis)(points))
          }
        })
      }

      function dragEnd () {
        // 拖拽结束
        dragging = false
      }

      // 交叉位置
      function intersectRect (node, point) {
        console.log(node)
        let x = node.x; let y = node.y; let dx = point.x - x; let dy = point.y - y; let w = node.guid === that.guid ? 24 : 21; let h = node.id === that.guid ? 24 : 21; let sx = 0; let sy = 0
        if (Math.abs(dy) * w > Math.abs(dx) * h) {
          dy < 0 && (h = -h)
          sx = dy === 0 ? 0 : h * dx / dy
          sy = h
        } else {
          dx < 0 && (w = -w)
          sx = w
          sy = dx === 0 ? 0 : w * dy / dx
        }
        return {
          x: x + sx,
          y: y + sy
        }
      }
    },
    // 渲染视图
    renderGraph () {
      this.initGraph().generateData().createGraph()
    },
    // 生成数据
    generateData () {
      // 节点连接样式
      const styleObjLeft = { fill: 'none', stroke: '#ffb203', width: 3 }
      const styleObjRight = { fill: 'none', stroke: '#FB4200', width: 3 }
      // 设置节点以及连接关系
      Object.keys(this.relationshipMap).forEach(t => {
        // 判断在节点的位置对应的连接样式
        const styleObj = this.nodeMap[t].isRight ? styleObjRight : styleObjLeft
        // 设置节点
        this.g._nodes[t] || this.g.setNode(t, this.nodeMap[t])
        // 设置连接的节点
        this.relationshipMap[t].forEach(m => {
          this.g._nodes[m] || this.g.setNode(m, this.nodeMap[m])
          // 连接
          this.g.setEdge(t, m, {
            arrowhead: 'arrowPoint',
            curve: d3.curveBasis,
            style: this.getStyleObjStr(styleObj),
            styleObj: styleObj,
            to: m
          })
        })
      })

      return this
    },
    // 生成对应关系
    crateLineageRelationshipHashMap (relations) {
      let map = {}

      relations.forEach(t => {
        map[t.fromEntityId] ? map[t.fromEntityId].push(t.toEntityId) : (map[t.fromEntityId] = [t.toEntityId])
      })

      return map
    },
    // 生成相应的数据
    crateGuidEntityHashMap (guidEntityMap) {
      let map = {}
      // 将数据点右侧数据整理
      this.resetRightMap(this.guid, this.relationshipMap, guidEntityMap, map)
      // 将数据点左侧数据整理
      this.resetLeftMap(guidEntityMap, map)
      // 返回数据
      return map
    },
    // 处理节点右侧数据
    resetRightMap (guid, relationshipMap, guidEntityMap, map) {
      const currentEntity = guidEntityMap[guid]
      const arr = relationshipMap[guid] ? relationshipMap[guid] : []

      map[guid] = {
        isLeaf: arr.length === 0,
        isRight: true,
        shape: 'img',
        typeName: currentEntity.typeName,
        guid: currentEntity.guid,
        label: currentEntity.displayText.slice(0, 15).concat('...')
      }

      arr.forEach(t => {
        this.resetRightMap(t, relationshipMap, guidEntityMap, map)
      })
    },
    // 处理节点左侧数据
    resetLeftMap (guidEntityMap, map) {
      Object.keys(guidEntityMap).forEach(t => {
        if (!map[t]) {
          map[t] = {
            isLeaf: false,
            isRight: false,
            shape: 'img',
            typeName: guidEntityMap[t].typeName,
            guid: guidEntityMap[t].guid,
            label: guidEntityMap[t].displayText.slice(0, 15).concat('...')
          }
        }
      })
    },
    // 样式生成器
    getStyleObjStr (styleObj) {
      return `fill: ${styleObj.fill};stroke: ${styleObj.stroke};stroke-width: ${styleObj.width}`
    },
    // base64转码
    getUrlBase64 (url, ext, callback) {
      var canvas = document.createElement('canvas') // 创建canvas DOM元素
      var ctx = canvas.getContext('2d')
      var img = new Image()
      img.crossOrigin = 'Anonymous'
      img.src = url
      img.onload = function () {
        canvas.height = 100 // 指定画板的高度,自定义
        canvas.width = 100 // 指定画板的宽度，自定义
        ctx.drawImage(img, 0, 0, 100, 100) // 参数可自定义
        const dataURL = canvas.toDataURL('image/' + ext)
        callback.call(this, dataURL) // 回掉函数获取Base64编码
        canvas = null
      }
    }
  }
}
</script>

<style lang="scss">
  g .node {
    cursor: pointer;
  }
  g .label {
    font-size: 12px;
  }
</style>

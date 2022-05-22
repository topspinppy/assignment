# 02 - Database Design

## Indexing
เป็นการจัดระเบียบการค้นหาข้อมูลใน Table หรือ Collection เพื่อทำให้ ประสิทธิภาพในการ Query ใน Database ไวขึ้น

โดย Use Case ที่เคยพบปัญหา คือ ระบบ มี Parcel Table ที่เก็บอยู่ในระบบ Query ด้วย Consignment Key (เลขพัสดุ) ได้ช้าและทำให้หน้าเว็บรอนาน รอนานจน Api / DB Timeout และในขณะนั้นใช้ library sequelize.js (ORM) ใน Project

วิธีแก้ปัญหาคือ generate file migration ที่ sequalize.js มีมาให้ และใช้คำสั่ง add Index ของ sequelize ดังตัวอย่าง

```js
queryInterface.addIndex('parcel', ['consignment'])
```
ซึ่งเทียบได้กับการ เขียนคำสั่ง SQL สำหรับ Add Index ในตาราง Parcel คือ
```sql
ALTER TABLE parcel ADD KEY (consignment);
```


## Normalization

เป็นการลดความซ้ำซ้อนและยุ่งยากของตาราง ที่เกินความจำเป็น และทำให้ตารางกระทัดรัด (compact) มากขึ้น โดย use case ที่เคยพบตอน design database คือ ต้องการออกแบบว่าคลังสินค้า (warehouse) มีรายละเอียดที่อยู่อะไรบ้าง (address)

ตัวอย่างตาราง warehouse (Full)

| warehouseId | name | address  | postcode | coordinate | lat | lng |
|-------------|------|----------|----------|------------|-----|-----|
| WH3001      | DCBB | บางบัวทอง | 20001    | 10         | 100 | 10  |
| WH3002      | DCMC | มหาชัย    | 30001    | 100        | 100 | 30  |
| WH3003      | DCSB | สุวรรณภูมิ  | 10540    | 10         | 150 | 10  |

ซึ่งตาราง warehouse ดังตัวอย่าง จะเห็นว่ามันมีข้อมูลที่สามารถแยกออกมาได้คือ Address ซึ่งจะได้ออกมาเป็นตารางใหม่ดังนี้

| addressId | address  | postcode | coordinate | lat | lng |
|-----------|----------|----------|------------|-----|-----|
| 0001      | บางบัวทอง | 20001    | 10         | 100 | 10  |
| 0002      | มหาชัย    | 30001    | 100        | 100 | 30  |
| 0003      | สุวรรณภูมิ  | 10540    | 10         | 150 | 10  |

หากทำการแยก address ออกมาเป็นอีกตารางแล้ว หน้าตาของตาราง warehouse จะออกมาเป็นดังนี้

| warehouseId | name | addressId|
|-------------|------|----------|
| WH3001      | DCBB | 0001     | 
| WH3002      | DCMC | 0002     | 
| WH3003      | DCSB | 0003     | 

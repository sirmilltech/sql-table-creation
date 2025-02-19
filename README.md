TO CREATE A NEW SQL FROM SCRATCH

create table items(
	item varchar(20),
	unitWeight integer,
	primary key (item)
);

create table busEntities(
	entity varchar(20),
	shipLoc varchar(20),
	address varchar(50),
	phone varchar(20),
	web varchar(50),
	contact varchar(20),
	primary key (entity)
);


create table billOfMaterials(
	prodItem varchar(20),
	matItem varchar(20),
	QtyMatPerItem integer,
	primary key (prodItem,matItem),
	foreign key (prodItem) references items (item),
	foreign key (matItem) references items (item)
);

create table supplierDiscounts(
	supplier varchar(20),
	amt1 decimal(8,4),
	disc1 decimal(3,2), 
	amt2 decimal(8,4),
	disc2 decimal(3,2),
	primary key (supplier),
	foreign key (supplier) references busEntities (entity)
);

create table supplyUnitPricing(
	supplier varchar(20), 
	item varchar(20),
	ppu integer,
	primary key (supplier,item),
	foreign key (supplier) references busEntities (entity),
	foreign key (item) references items
);

create table manufDiscounts(
	manuf varchar(20),
	amt1 decimal(8,4),
	disc1 decimal(3,2),
	primary key (manuf),
	foreign key (manuf) references busEntities (entity)
	
);

create table manufUnitPricing(
	manuf varchar(20),
	prodItem varchar(20),
	setUpCost integer,
	prodCostPerUnit integer,
	primary key(manuf,prodItem),
	foreign key (manuf) references busEntities (entity),
	foreign key (prodItem) references items 
);

create table shippingPricing(
	shipper varchar(20),
	fromLoc varchar(20),
	toLoc varchar(20),
	minPackagePrice integer,
	pricePerLb integer,
	amt1 integer,
	disc1 integer,
	amt2 integer,
	disc2 integer,
	primary key(shipper,fromLoc,toLoc),
	foreign key (shipper) references busEntities (entity)
);

create table customerDemand(
	customer varchar(20),
	item varchar(20),
	qty integer,
	primary key(customer,item),
	foreign key(item) references items,
	foreign key (customer) references busEntities (entity)
);

create table supplyOrders(
	item varchar(20),
	supplier varchar(20),
	qty integer,
	primary key(item,supplier),
	foreign key(item) references items,
	foreign key(supplier) references supplierDiscounts
);

create table manufOrders(
	item varchar(20),
	manuf varchar(20),
	qty integer,
	primary key(item,manuf),
	foreign key(item) references items,
	foreign key(manuf) references manufDiscounts
);

create table shipOrders(
	item varchar(20),
	shipper varchar(20),
	sender varchar(20),
	recipient varchar(20),
	qty integer,
	primary key(item, shipper, sender, recipient),
	foreign key(item) references items,
	foreign key(shipper) references busEntities (entity),
	foreign key (sender) references busEntities (entity),
	foreign key (recipient) references busEntities (entity)
);



select * From INFORMATION_SCHEMA.TABLE_CONSTRAINTS


select* from items, busEntities, billOfMaterials

E-COMMERCE PROJECT ANALYSIS
This  project is about the analysis of e-commerce industry where we see some insights based on customer purchasing behaviour.
ABOUT DATA : THIS DATA HAS FOLLWING COLUMNS
1.CUSTOMER ID: REPRSENT THE EACH CUSTOMER
2.AGE : RESPRESENT AGE OF CUSTOMER
3.GENDER : REPRSENT CUSTOMER GENDER AND THE PURCHASING BEHAVIOUR
4.LOCATION : SHOWS THE COUNTRY FROM WHICH PRODUCTS ARE PURCHASED
5.PRODUCT CATEGORY : DIFFERENT CATEGORIES OF PRODUCT BASED ON THEIR PRODUCT NAME
6.PURCHASE AMOUNT : AMOUNT SPEND ON PURCHASE
7.PURCHASE DATE : DATE ON WHICH PRODUCTS ARE PURCHAS
8.PAYEMENT METHOD : THE TYPE OF PAYEMENT OPTION USED FOR PAYING PAYPAL , CASH , CREDITCARD , DEBIT  CARD
9.DEVICE USED : REPRESENT WHICH DEVICE USED TO DO PURCHASING MOBILE , DESKTOP, TABLET
10.RETURNING CUSTOMER : IF THE CUSTOMER IS NEW OR RETURNING 0 REPRESENT RETURNING CUSTOMER AND 1 REPRESENT NEW CUSTOMNE
--Data cleaning --

select* from Global_Ecommerce_Customer_Behavior where CustomerID is null or Age is null or Gender is null or Location is null or ProductCategory 
is null or PurchaseAmount is null or PaymentMethod is null or PurchaseDate is null or DeviceUsed is null or ReturningCustomer is null ;

--- remove duplicate --

delete from Global_Ecommerce_Customer_Behavior where Age in (select Age from Global_Ecommerce_Customer_Behavior group by Age having count (*) > 1);

rollback;


-- there are some insight --

---  total sales by country--

select Location , sum (PurchaseAmount) as Totalsales from Global_Ecommerce_Customer_Behavior group by Location order by Totalsales desc;

-- males vs female purchase --

select Gender , count (*) as TotalOrders,avg(PurchaseAmount) as avgSpend from Global_Ecommerce_Customer_Behavior group by Gender;

-- top 5 --

 select top 5 * from Global_Ecommerce_Customer_Behavior;

 -- total number off customers--
 select count (*) from Global_Ecommerce_Customer_Behavior;

 -- most used payment--

 select PaymentMethod, count (*) from Global_Ecommerce_Customer_Behavior group by PaymentMethod;
  
   -- wich product are max , min --
  select max (ProductCategory) as max_category from Global_Ecommerce_Customer_Behavior;
  select min (ProductCategory) as max_category from Global_Ecommerce_Customer_Behavior;
  
  --average spending by gender --

  select Gender ,AVG ( PurchaseAmount) from Global_Ecommerce_Customer_Behavior group by Gender;

  -- window function--

  -- rn function--

  select *,ROW_NUMBER() over (order by Gender desc) as rn_number from Global_Ecommerce_Customer_Behavior;

  -- lag-- 

  select Gender,PurchaseAmount, LAG (PurchaseAmount ) over (order by Gender ) as prev_price from Global_Ecommerce_Customer_Behavior;

  ---rank ---

  select PaymentMethod,PurchaseAmount ,rank () over ( order by PaymentMethod desc) as most_use_rank  from Global_Ecommerce_Customer_Behavior;

  -- dense rank--

  select PaymentMethod,PurchaseAmount ,dense_rank () over (order by  PurchaseAmount  desc)as dense_rank from Global_Ecommerce_Customer_Behavior;



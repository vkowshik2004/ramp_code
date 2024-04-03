# ramp_code
Code to compute 3 day rolling average

https://www.db-fiddle.com/f/fid98sBC4wwiQ5gLAkiCya/1

;WITH BASE_TABLE AS ( 
  SELECT 
  	CAST(transaction_time AS DATE) transaction_date 
  	,SUM(transaction_amount) transaction_amount 
  FROM TRANSACTIONS 
  GROUP BY CAST(transaction_time AS DATE)
) 

SELECT 
	transaction_date 
    ,AVG(transaction_amount) 
    	OVER (ORDER BY transaction_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) THREE_DAY_ROLLING_AVG 
FROM BASE_TABLE 
ORDER BY 1

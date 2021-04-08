# StreamingSQLDemos
Demos on stonks



#### Weather

select location, max(temp_f) as max_temp_f, avg(temp_f) as avg_temp_f, min(temp_f) as min_temp_f from weather2 
group by location

#### SCADA

#### Energy

#### Stocks

SELECT symbol, uuid, ts, dt, `open`, `close`, high, volume, `low`, `datetime`, 'new-high' message, 
'nh' alertcode, CAST(CURRENT_TIMESTAMP AS BIGINT) alerttime 
FROM stocksraw st 
WHERE symbol is not null 
and symbol <> 'null' and
trim(symbol) <> '' and 
CAST(`close` as DOUBLE) > 
(SELECT MAX(CAST(`close` as DOUBLE)) FROM stocksraw s 
WHERE s.symbol = st.symbol)



SELECT scada.uuid, scada.systemtime, scada.temperaturef, scada.pressure, scada.humidity, scada.lux, scada.proximity, 
scada.oxidising,scada.reducing , scada.nh3, scada.gasko,energy.`current`, energy.voltage,energy.`power`,energy.`total`,energy.fanstatus
FROM energy JOIN scada ON energy.systemtime = scada.systemtime;


SELECT CAST(symbol as STRING) symbol, CAST(uuid as STRING) uuid, ts, dt, open, close, high, volume, low, datetime, 'new-high' message, 'nh' alertcode, CAST(CURRENT_TIMESTAMP AS BIGINT) alerttime FROM stocks st WHERE symbol is not null and symbol <> 'null' and trim(symbol) <> '' and CAST(close as DOUBLE) > (SELECT MAX(CAST(close as DOUBLE)) FROM stocks s WHERE s.symbol = st.symbol);

SELECT scada2.uuid, scada2.systemtime, scada2.temperaturef, 
scada2.pressure, scada2.humidity, scada2.lux, scada2.proximity, 
scada2.oxidising,scada2.reducing , scada2.nh3, 
scada2.gasko, energy2.voltage,energy2.total,energy2.fanstatus 
FROM energy2, scada2 
WHERE energy2.systemtime = scada2.systemtime

# event status

select * 
from statusevents
where lower(description) like '%fail%' or lower(description) like '%error%'

# funcion en manteminiento 

go
create function dbo.mElsQuedo2(@njugador int , @punts int )
returns bit
as begin
declare @si bit;
declare @puntosally int;
declare @puntosenemy int;
declare @diferencia int;

set @puntosally =(select SUM (puntsanotats) from marcador
				  where njugadoranota = 1)
set @puntosenemy =(select SUM (puntsanotats) from marcador
				  where njugadoranota = 2)

set @diferencia = (@puntosally - @puntosenemy)

if @puntosally > @puntosenemy and @diferencia > @punts set @si = 0
else set @si = 1				

return @si 
end

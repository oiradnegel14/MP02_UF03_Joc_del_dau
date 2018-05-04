# Definitiu

La meva estrategia serà quedar-me el número si és 4 o més gran, si no li donaré el número a l'altre. En cas de que vagi perdent, agafaré els daus de 2 o més.

```

create function melsquedo(@jugador as int, @punts as int)
returns bit
as begin
	declare @quedat as bit, @marcador_meu as int, @marcador_altre as int;
	set @marcador_meu=(select sum(puntsAnotats) from marcador where nJugadorAnota=@jugador)
	set @marcador_altre=(select sum(puntsAnotats) from marcador where nJugadorAnota!=@jugador)
	if @punts>=4 begin
		set @quedat=1;
	end
	else if @marcador_altre>@marcador_meu and @punts>=2 begin
		set @quedat=1;
	end
	else
		set @quedat=0;
	return @quedat
end

```

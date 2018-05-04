# Bits en el ring. Contienda. Dado.David Ayachi
Ens en demanaven que féssim una funció de si ens quedem el número obtingut o no.Jo el que he fet és si el número obtingut és entre 0 i 3 li donem a la altra persona. En el cas que sigui més gran de 3 mels quedo jo. 
<br>He fet el joc amb si, si el voleu, està adjuntat al meu perfil.
```
CREATE FUNCTION dbo.Melsquedo (@nJugador  AS INT, 
                               @punts    AS INT) 
returns INTEGER 
AS 
  BEGIN 
      DECLARE @siono        INT, 
              @puntjugador1 INT, 
              @puntjugador2 INT; 

      SET @puntjugador1=(SELECT Sum(puntsAnotats  + @punts) 
                         FROM   marcador 
                         WHERE  nJugadorAnota = @nJugador ) 
      SET @puntjugador2=(SELECT Sum(puntsAnotats  + @punts) 
                         FROM   marcador 
                         WHERE  nJugadorAnota != @nJugador ) 

      IF @puntjugador1 >= @puntjugador2 
        BEGIN 
            SET @siono=1 
        END; 
      ELSE 
        BEGIN 
            SET @siono=0 
        END; 

      RETURN @siono 
  END; 
  Go;
```

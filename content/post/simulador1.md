---
title: "Simulador Economía Chilena - En Construcción"
date: 2019-10-02T01:00:39-03:00
draft: false
tags: ["simulador", "economia", "chile", "estadisticas"]


---

<link rel="stylesheet" href="https://unpkg.com/tachyons@4.10.0/css/tachyons.min.css"/>

<p style="text-align:justify;">
El siguiente post tiene como objetivo describir la metodología
utilizada para la construcción del simulador de Shocks sobre la economía Chilena.
</p>
<!--more-->




<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>


<style>
.zebra-striping tbody tr:nth-child(odd) {
  background: #eee;
}
</style>

<div class="ox-hugo-table zebra-striping sane-table">
<div></div>

**Matriz de insumo producto**

* Matriz de Insumo Producto : matriz que contiene el equilibrio entre la oferta y la utilización de bienes y servicios en un periodo determinado de tiempo

<div>

<table>
	<tbody>
		<tr>
			<td rowspan="2"><b>Compras/Ventas</b></td>
			<td colspan="3"><b><center>Demanda Intermedia</center></b></td>
			<td rowspan="2"><b>Demanda Final</b></td>
			<td rowspan="2"><b>Producción Bruta</b></td>
		</tr>
		<tr>
			<td><b>Agricultura</b></td>
			<td><b>Industria</b></td>
			<td><b>Servicios</b></td>
		</tr>
		<tr>
			<td>Agricultura</td>
			<td>100</td>
			<td>200</td>
			<td>300</td>
			<td>100</td>
			<td>700</td>
		</tr>
		<tr>
			<td>Industria</td>
			<td>500</td>
			<td>300</td>
			<td>200</td>
			<td>200</td>
			<td>1200</td>
		</tr>
		<tr>
			<td>Servicios</td>
			<td>400</td>
			<td>100</td>
			<td>600</td>
			<td>500</td>
			<td>1600</td>
		</tr>
	</tbody>
</table>

</div>


<p style="text-align:justify;">
En el caso chileno, estas matrices se encuentran disponibles en el siguiente link:

</p>


[MIPs - Banco Central](https://si3.bcentral.cl/estadisticas/Principal1/Informes/anuarioCCNN/index_anuario_CCNN_2018.html?chapterIdx=-1&curSubCat=-1 "Title").

<p style="text-align:justify;">
Para explicar la relación existente entre la producción total de la economía, la demanda final y la demanda intermedia se introducirá la siguiente notación matricial.

</p>


<p style="text-align:justify;">

Con <b>Pi</b> se representará la producción total de la <b>actividad "i":</b>

</p>

<div>$$\begin{pmatrix}
	{P_{1}}\\
	{P_{2}}\\
	{P_{3}}\end{pmatrix}
	\begin{pmatrix}
	{700}\\
	{1200}\\
	{1600}\end{pmatrix}
	$$
</div>


<p style="text-align:justify;">

Con <b>yi</b> se representará la demanda final asociada a la **actividad económica "i"**:

</p>



<div>$$
	\begin{pmatrix}
	{y_{1}}\\
	{y_{2}}\\
	{y_{n}}\end{pmatrix}
	\begin{pmatrix}
	{100}\\
	{200}\\
	{500}\end{pmatrix}$$
</div>

Con **xij** se representará a las compras/ventas entre sectores



<div>$$
	\begin{pmatrix}
    {x_1}_1 & {x_1}_2  & {x_1}_3 \\\ 
    {x_2}_1 & {x_2}_2 & {x_2}_3\\
    {x_3}_1 & {x_3}_2 & {x_3}_3 
    \end{pmatrix}

    \begin{pmatrix}
    100 & 200  & 300 \\\ 
    500 & 300 & 200\\
    400 & 100 & 600 
    \end{pmatrix}$$
</div>

Con estas definiciones, la producción total, en términos matriciales, puede ecribirse como:

$$P = X \cdot 1_{n}  + y $$

En donde $$1_{n}$$ corresponde a un vector columna de "1" de tamaño n.


**Coeficiente Técnico**

<p style="text-align:justify;">

Es la relación existente entre insumos y producción total de cada actividad. Representa la cantidad necesaria de un bien (insumos), para producir otro bien (producto). 

Por ejemplo, para el caso de la industria del pan, esta podría estar adquiriendo trigo desde el sector agricultor para la producción de pan. Se podría llegar a una relación monetaria de cuanto de trigo ($) se necesita para producir una unidad de pan($).

En el corto plazo, ante la no presencia de cambios tecnológicos en los procesos productivos, se puede asumir que esta relación es relativamente constante, siendo este uno de los principales supuestos del simulador de "Shocks".

Cada coeficiente técnico se denotará como <b>aij</b>, en donde para el caso de la primera columna, se tiene lo siguiente:

</p>

<div>$$
	\begin{pmatrix}
	{a_1}_1\\
	{a_2}_1\\
	{a_3}_1\end{pmatrix}
	=
	\begin{pmatrix}
	\frac{{x_1}_1}{P_{1}}\\
	\frac{{x_1}_1}{P_{1}}\\
	\frac{{x_1}_1}{P_{1}}\end{pmatrix}
	=
	\begin{pmatrix}
	\frac{{x_1}_1}{P_{1}}\\
	\frac{{x_1}_1}{P_{1}}\\
	\frac{{x_1}_1}{P_{1}}\end{pmatrix}$$
</div>




<p style="text-align:justify;">

Considerando las demás columnas, se define la matriz de <b>A</b> de coeficientes técnicos:

</p>


<div>$$
	\begin{pmatrix}
    {a_1}_1 & {a_1}_2  & {a_1}_3 \\\ 
    {a_2}_1 & {a_2}_2 & {a_2}_3\\
    {a_3}_1 & {a_3}_2 & {a_3}_3 
    \end{pmatrix}
$$
</div>





Por lo tanto, esta ecuación:


$$P = X \cdot 1_{n}  + y  $$

Puede escribirse como:

$$P = A \cdot P  + y $$

Con un poco de algebra matricial se llega a que:


$$P = (I-A)^{-1} \cdot y $$

Esta última relación es la base matemática para el cálculo de los "shocks" sobre la economía chilena.

**Nota:**

$$ (I-A) = Matriz \ de \ Leontief $$
$$ (I-A)^{-1} = Matriz \ inversa \ de \ Leontief $$

**¿Por qué?**

<p style="text-align:justify;">

Porque simulando un nuevo vector "y" de consumos finales, por ejemplo una caída de las exportaciones (debido a una baja demanda de cobre de China) es posible conocer los nuevos niveles de producción "P" asociados a esta baja en la demanda de minería. Esta simulación no solo permite conocer el nuevo nivel asociado a la minería debido a esta baja en la demanda, sino que el efecto de "encadenamiento productivo" sobre la economía total.

</p>


**Encadenamiento productivo**

<p style="text-align:justify;">



Una caída en la demanda de cobre no sólo tendrá un efecto directo en la producción nacional de la minería, sino que debido a que la Industria Minera demanda insumos de los Servicios (por ejemplo, Servicios de Ingeniería), provocará una baja en la producción de Servicios.Por otro lado, las empresas de Servicios de Ingeniería, demandan a su vez otras empresas de Servicios de Ongeniería para la generación de su producción, esto provocará una caída en la actividad sobre si misma. Este efecto de encadenamiento se va diluyendo en cada iteración. La relación matricial para obtener los nuevos nivel de producción "Pi" permite calcular el efecto final de estos encadenamientos y obtener los nuevos niveles de equilibrio de producción de todos los sectores económicos.
</p>



----------------------------



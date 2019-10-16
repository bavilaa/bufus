---
title: "Simulador Economía Chilena"
date: 2019-10-02T01:00:39-03:00
#draft: true
tags: ["simulador", "economia", "chile", "estadisticas"]


---





El siguiente post tiene como objetivo describir la metodología
utilizada para la construcción del simulador de Shocks sobre la economía Chilena.
</p>
<!--more-->




<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

<h3>Definiciones</h3>

<style>
.zebra-striping tbody tr:nth-child(odd) {
  background: #eee;
}
</style>

<div class="ox-hugo-table zebra-striping sane-table">
<div></div>



* Matriz de Insumo Producto : matriz que contiene todas las 
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





Para la economía Chilena, estas matrices se encuentran disponibles en el siguiente link:  [MIPs - Banco Central](https://si3.bcentral.cl/estadisticas/Principal1/Informes/anuarioCCNN/index_anuario_CCNN_2018.html?chapterIdx=-1&curSubCat=-1 "Title").


Para explicar la relación existente entre la producción total de la economía, la demanda final y la demanda intermedia se introdirá la siguiente notación matricial.

Con **Xi** se representará la producción total de la **actividad "i"**: 



<div>$$\begin{pmatrix}
	{X_{1}}\\
	{X_{2}}\\
	\vdots\\
	{X_{n}}\end{pmatrix}
	\begin{pmatrix}
	{X_{1}}\\
	{X_{2}}\\
	\vdots\\
	{X_{n}}\end{pmatrix}
	$$
</div>

<div>$$\begin{pmatrix}
	{X_{1}}\\
	{X_{2}}\\
	{X_{3}}\end{pmatrix}
	\begin{pmatrix}
	{700}\\
	{1200}\\
	{1600}\end{pmatrix}
	$$
</div>



Con **yi** se representará la demanda final asociada a la **actividad económica "i"**:

<div>$$\begin{pmatrix}
	{y_{1}}\\
	{y_{2}}\\
	\vdots\\
	{y_{n}}\end{pmatrix}$$
</div>


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

$$\begin{pmatrix} X_{11} & 66 \\\ c & d\end{pmatrix}$$

$$\binom{xi}{{X_{11}}}$$



Recordando que para el caso de la apertura de la Matriz Chilena el consumo total corresponde a :



$$
	\begin{align}
	Consumo \ Total = Consumo \ de\ hogares + Consumo\ de\ IPSFL  \newline + 
	Consumo \ de \ gobierno \ Formación \ Bruta \ de \ Capital Fijo +\newline  
	Variación de Existencia + Exportaciones
	\end{align}
$$


Por lo tanto, la matriz de insumo producto puede escribirse como:

$$X = AX + y $$

Conteniendo las producciones totales de la actividad 1, 2 ... n (n=12 para el caso del simulador)








\begin{align}
\dot{x} & = \sigma(y-x) penita \newline
\dot{y} & = \rho x - y - xz \newline
\dot{z} & = -\beta z + xy
\end{align}


$$\sqrt{3x-1}+(1+x)^2$$


$$
\begin{align}
  \nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} & = \frac{4\pi}{c}\vec{\mathbf{j}} \newline
  \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \newline
  \nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \newline
  \nabla \cdot \vec{\mathbf{B}} & = 0
\end{align}
$$



$$\begin{pmatrix}a & b\\\ c & d\end{pmatrix}$$

$$\binom{xi}{x}$$





$$\begin{pmatrix}{X_{1}}\end{pmatrix}$$


$$
\begin{eqnarray} 
y &=& x^4 + 4      \nonumber \\
  &=& (x^2+2)^2 -4x^2 \nonumber \\
  &\le&(x^2+2)^2    \nonumber
\end{eqnarray} 
$$
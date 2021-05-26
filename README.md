#include <iostream>
using namespace std;
int const filas = 4;
int const columnas = 5;
void imprimirMatrizBoleanos(bool matrizDisponibilidad[filas][columnas]);
void limpiarMatrices(bool disponibilidad[filas][columnas], int pesos[filas][columnas]);
void imprimirMatrizTexto(string matriz[filas][columnas]);
void imprimirMatrizNumeros(int matriz[filas][columnas]);
int contenedormenosPesado(int pesos[filas][columnas]);
void valorRecaudadoPuerto(string puertocarga[filas][columnas], string puertoa);
void mostrar(bool disponibilidad[filas][columnas]);
float promedioPeso(int pesos[filas][columnas]);
int filamasllena(int pesos[filas][columnas]);
int columnamenosllena(int pesos[filas][columnas]);
float calcularOcupacion(bool disponibilidad[filas][columnas]);
float promedioPesoPuerto(int pesos[filas][columnas], string puertoCarga[filas][columnas], string puertoBuscado);
int cantidadTipoArticulo(string tipoArticulo[filas][columnas], string tipoArticuloBuscado);
string nombreEmpresaContenedorMasPesado(int pesos[filas][columnas], string marcas[filas][columnas]);
void imprimirCantidadContenedores(bool disponibilidad[filas][columnas]);

int main()
{
    int Npuertos=0;
    cout <<"ingrese la cantidad de puertos" <<endl;
    cin>>Npuertos;
    string nombres[Npuertos];
    for (int i = 0; i < Npuertos; i++)
    {
        cout <<"ingrese nombre de los puertos " << endl;
        cin >>nombres[i];
    }
    int pesoMenor =0;
    int posicionI = 0;
    int posicionJ = 0;
    int ocupaciondelbarco = 0;
    int filaMayorValor = 0;
    int filaMasLlena = 0;
    int ColumnamLlena = 0;
    float promedioPesos = 0.0;
    int cantidadArticulo=0;
    string nombre;
    bool valido = 0;
    float promedioPesodePuerto = 0.0;
    bool disponibilidad[filas][columnas];
    string marcas[filas][columnas];
    string puertocarga[filas][columnas];
    string tipoArticulo[filas][columnas];
    int pesos[filas][columnas];
    limpiarMatrices(disponibilidad, pesos);
    for(int i=0;i<Npuertos;i++)
    {
    	cout<<"                                                                      ----- bienvenido al puerto "<<nombres[i]<<"---- "<<endl;
    	int contenedores=0;
    	cout<<"ingrese cuantos contenedores "<<endl;
    	cin>>contenedores;
    	for(int j=0;j<contenedores;j++)
    	{
    		int valorTotal=0;
    		do{
    			mostrar(disponibilidad);
    			cout<<"ingrese el valor de filas"<<endl;
    			cin>>posicionI;
    			cout<<"ingrese el valor de columnas "<<endl;
    			cin>>posicionJ;
    			if(posicionI>=0 && posicionI<filas && posicionJ>=0 && posicionJ<columnas)
    			{
    				if(disponibilidad[posicionI][posicionJ]==1)
    				{
    					disponibilidad[posicionI][posicionJ]=0;
    					valido=1;
					}
					else
					{
						valido=0;
					}
				}
				else
				{
					valido=0;
				}
			}while(valido==0);
			cout<< "puerto marcas " <<endl;
            cin>> marcas[posicionI][posicionJ];
            cout<< "puerto carga " <<endl;
            cin>> puertocarga[posicionI][posicionJ];
            cout<<"peso "<<endl;
            cin>>pesos[posicionI][posicionJ];
            cout<<"tipo articulo "<<endl;
            cin>>tipoArticulo[posicionI][posicionJ];
		}
		valorRecaudadoPuerto(puertocarga,nombres[i]);
	}
	cout << "matriz disponiblidad " << endl;
    imprimirMatrizBoleanos(disponibilidad);

    cout << " matriz marcas " << endl;
    imprimirMatrizTexto(marcas);
    cout << "matriz puerto carga " << endl;
    imprimirMatrizTexto(puertocarga);
    cout << "matriz tipo articulo " << endl;
    imprimirMatrizTexto(tipoArticulo);
    cout << "matriz peso " << endl;
    imprimirMatrizNumeros(pesos);
    
    string tipoArticuloBuscado="";
    cout<<"ingrese articulo a buscar "<<endl;
    cin>>tipoArticuloBuscado;
    
    string puertoBuscado="";
    cout<<"ingrese el puerto a buscar "<<endl;
    cin>>puertoBuscado;
    
    contenedormenosPesado(pesos);
    pesoMenor=contenedormenosPesado(pesos);
    cout<<"el contenedor menos pesado es "<<pesoMenor<<endl;
    
    calcularOcupacion(disponibilidad);
    ocupaciondelbarco=calcularOcupacion(disponibilidad);
    cout << "Ocupacion Del Barco Actual " << ocupaciondelbarco <<"%"<<endl;
    
    filamasllena(pesos);
    filaMasLlena=filamasllena(pesos);
    cout<<"la fila mas llena es "<<filaMasLlena<<endl;
    
    columnamenosllena(pesos);
    ColumnamLlena=columnamenosllena(pesos);
    cout<<"la columna menos llena es "<<ColumnamLlena<<endl;
    
    promedioPeso(pesos);
    promedioPesos=promedioPeso(pesos);
    cout<<"el promedio de los pesos es "<<promedioPesos<<endl;
    
    promedioPesoPuerto(pesos,puertocarga,puertoBuscado);
    promedioPesos=promedioPesoPuerto(pesos,puertocarga,puertoBuscado);
    cout<<" el promedio del puerto es "<<promedioPesos<<endl;
    
    cantidadTipoArticulo(tipoArticulo,tipoArticuloBuscado);
    cantidadArticulo=cantidadTipoArticulo(tipoArticulo,tipoArticuloBuscado);
    cout<<" la cantidad del articulo buscado es "<<cantidadArticulo<<endl;
    
    nombreEmpresaContenedorMasPesado(pesos,marcas);
    nombre=nombreEmpresaContenedorMasPesado(pesos,marcas);
    cout<<"el nombre de la empresa con mas peso es "<<nombre<<endl;
    imprimirCantidadContenedores(disponibilidad);
	return 0;
}
void limpiarMatrices(bool disponibilidad[filas][columnas], int pesos[filas][columnas])
{
    for (int i=0;i<filas;i++){
        for (int j=0;j<columnas;j++){
            disponibilidad[i][j]=1;
            pesos[i][j]=0;
        }
    }
}
void imprimirMatrizBoleanos(bool matriz[filas][columnas])
{
    for (int i=0;i<filas;i++){
        for (int j=0;j<columnas;j++){
            cout<<matriz[i][j] <<"\t";
        }
        cout<<endl;
    }
}
void imprimirMatrizTexto(string matriz[filas][columnas])
{
    for (int i = 0; i < filas; i++){
        for (int j = 0; j < columnas; j++){
            cout << matriz[i][j] << "\t";
        }
        cout<<endl;
    }
}
void imprimirMatrizNumeros(int matriz[filas][columnas])
{
    for (int i=0;i<filas;i++){
        for (int j=0;j<columnas;j++){
            cout<<matriz[i][j] <<"\t";
        }
        cout<<endl;
    }
}

//procesos
//punto 1
void imprimirCantidadContenedores(bool disponibilidad[filas][columnas])
{
    int contador=0;
    for (int i=0;i<filas;i++){
        for (int j=0;j<columnas;j++){
        	if(disponibilidad[filas][columnas]==0){
        		contador=contador+1;
			}
        }
    }
    cout<<"la cantidad de contenedores es "<<contador<<endl;
}
//punto 2
void burbuja(string puertos[], int cantidadContenedores[])
{
}
//punto 3
void listadoMarcasEconomica(string marcas[filas][columnas], bool disponibilidad[filas][columnas])
{
	for (int i=0;i<filas;i++){
		for (int j=0;j<columnas;j++){
			if(disponibilidad[i][j]==0 && ((i==0 || i==3) || (j==0 || j==4))){
				cout<<marcas[i][j];
			}
		}
	}
}
//punto 4
void listadoMarcasPremium(string marcas[filas][columnas], bool disponibilidad[filas][columnas]){
	for (int i=0;i<filas;i++){
		for (int j=0;j<columnas;j++){
			if(disponibilidad[i][j]==0 && ((i==1 && j==1 || j==2 || j==3) || (i==2 && j==1 || j==2 || j==3))){
				cout<<marcas[i][j];
			}
		}
	}
}
//punto 5
void reporteMarca(string marcas[filas][columnas], string marcabuscada[])
{
}
//mostrar disponibilidad
void mostrar(bool disponibilidad[filas][columnas])
{
    for(int i=0;i<filas;i++)
    {
        for(int j=0;j<columnas;j++)
        {
            cout<<disponibilidad[i][j] << ",";
        }
        cout<<endl;
	}
}
//ocupacion del barco
float calcularOcupacion(bool disponibilidad[filas][columnas]){
	float ocupacion=0.0;
	int contador=0;
	for(int i=0;i<filas;i++){
		for(int j=0;j<columnas;j++){
			if(disponibilidad[i][j]==0){
				contador=contador+1;
			}
		ocupacion=(contador*100)/(filas*columnas);	
		}
	}
	return ocupacion;
}
//valor total del recaudo
void valorRecaudadoPuerto(string puertocarga[filas][columnas], string puertoa)
{
	int valorDecadaPuerto=0;
	for(int i=0;i<filas;i++){
		for(int j=0;j<columnas;j++){
			if(puertocarga[i][j]==puertoa){
				if(i==1 || i==2 && j==1 || j==2 || j==3){
					valorDecadaPuerto=valorDecadaPuerto+300;
				}else{
					valorDecadaPuerto=valorDecadaPuerto+100;
				}
			}
		}
	}
	cout<<" el valor es "<<valorDecadaPuerto<<endl;
}
//punto 6
float promedioPeso(int pesos[filas][columnas]){
	float promedio=0.0;
	int acumulador=0;
	int contador=0;
	for(int i=0;i<filas;i++){
		for(int j=0;j<columnas;j++){
			if(pesos[i][j]>2){
				acumulador=acumulador+pesos[i][j];
				contador=contador+1;
			}	
		}
		promedio=acumulador/contador;
	}
	return promedio;
}
// punto 7
int filamasllena(int pesos[filas][columnas]){
	int mayor=INT_MIN;
	int filaMayor=-1;
	int suma=0;
	for(int i=0;i<filas;i++){
		for(int j=0;j<columnas;j++){
			suma=suma+pesos[i][j];
		}
		if(suma>mayor){
			mayor=suma;
			filaMayor=i;
		}
		suma=0;
	}
	return filaMayor;
}
//punto 8
int columnamenosllena(int pesos[filas][columnas]){
	int menor=INT_MAX;
	int columnaMenor=-1;
	int suma=0;
	for(int i=0;i<columnas;i++){
		for(int k=0;k<filas;k++){
			suma=suma+pesos[k][i];
		}
		if(suma<menor){
			menor=suma;
			columnaMenor=i;
		}
		suma=0;
	}
	return columnaMenor;
}
//punto 9
int cantidadTipoArticulo(string tipoArticulo[filas][columnas], string tipoArticuloBuscado)
{
	int contadorarticulo=0;
	for(int i=0;i<filas;i++){
		for(int j=0;j<columnas;j++){
			if(tipoArticulo[i][j]==tipoArticuloBuscado){
				contadorarticulo=contadorarticulo+1;
			}
		}
	}
	return contadorarticulo;
}
//punto 10
float promedioPesoPuerto(int pesos[filas][columnas], string puertocarga[filas][columnas], string puertoBuscado)
{
	int acumuladorpesos=0;
	int contadorpesos=0;
	float promediopesos=0.0;
	for(int i=0;i<filas;i++){
		for(int k=0;k<columnas;k++){
			if(puertocarga[i][k]==puertoBuscado){
				acumuladorpesos=acumuladorpesos+pesos[i][k];
				contadorpesos=contadorpesos+1;
			}
		}
		promediopesos=acumuladorpesos/contadorpesos;
	}
	return promediopesos;
}
//punto 11
string nombreEmpresaContenedorMasPesado(int pesos[filas][columnas], string marcas[filas][columnas])
{
	int mayor=INT_MIN;
	string nombreEmpresa;
	for(int i=0;i<filas;i++){
		for(int k=0;k<columnas;k++){
			if(pesos[i][k]>mayor){
				mayor=pesos[i][k];
				nombreEmpresa=marcas[i][k];
			}
		}
	}
	return nombreEmpresa;
}
//punto 12
int contenedormenosPesado(int pesos[filas][columnas])
{
    int menor=INT_MAX;
    for (int i= 0;i<filas;i++){
        for (int j=0;j<columnas;j++){
            if (pesos[i][j]<menor){
                menor=pesos[i][j];
            }
        }
    }
    return menor;
}

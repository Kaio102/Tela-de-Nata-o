package com.example.sportgo

import androidx.compose.foundation..*
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.CircleShape
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

// FireBase Imports (Comentados Para Aula Futura)
// import com.google.firebase.firestore.FirebaseFirestore

@OptIl(ExperimentalMaterial3Api::class)
@Composable
fun TelaNatacao(
    onVoltar:()->Unit,
    onReservar:()->Unit
){
    //Logica FireBase(Comentada)
    /*
    val db=FirebaseFirestore.getInstance()
    var listaPiscinas by remember{mutableStateOf(listOf<Any>())}

    LaunchedEffect(Unit){
        db.collection("piscinas").get().addOnSuccessListener{result->//Carregar dados dinamicos aqui}
    }
}
*/
val corNatacao=Color(0xFF0288D1)//Azul Oceano
val corFundo=Color(0xFFF1F4F8)

Scaffold(
    topBar={
        TopAppBar(
            title={
                Column{
                    Text("Natação Community",color=Color.White,fontSize=18.sp,fontWeight=FontWeight.Bold)
                    Text("Mergulhe no seu próximo treino",color=Color.White.copy(0.8f),fontSize=12.sp)
                }
            },
            actions={
                IconButton(onClick=onVoltar){
                    Icon(Icons.Default.Waves,null,tint=Color.White)
                }
            },
            colors=TopAppBarDefaults.topAppBarColors(containerColor=corNatacao)
        )
    }
){padding->
Column(
    modifier=Modifier
    .fillMaxSize()
    .padding(padding)
    .background(corFundo)
    .verticalScroll(rememberScrollState())
) {
    //Container:Banner Imersivo
    Surface(
        modifier=Modifier
        .fillMaxWidth()
        .height(180.dp),
        color=Color(0xFF01579B)//Azul Profundo para o Banner
    ){
        Box(contentAlignment=Alignment.Center)
        //Placeholder para a foto de um nadador ou piscina limpida
        Text("IMAGEM NATAÇÃO",color=Color.White.copy(0.7f),fontWeight=FontWeight.Bold)
    }
  }
  //Container:Busca
  Card(
    modifier=Modifier
    .fillMaxWidth()
    .padding(16.dp),
    shape=RoundedCornerShape(12.dp),
    colors=CardDefaults.cardColors(containerColor=Color.White),
    elevation=CardDefaults.cardElevation(2.dp)
  ){
    OutlinedTextField(
        value="",
        onValueChange={},
        placeholder={Text("Buscar raias ou clubes...",fontSize=14.sp)},
        modifier=Modifier
        .fillMaxWidth()
        .padding(8.dp),
        shape=RoundedCornerShape(8.dp),
        leadingIcon={Icon(Icons.Default.Search,null,tint=corNatacao)},
        colors=OutlinedTextFieldDefaults.colors(
            unfocusedBorderColor=Color.Transparent,
            focusedBorderColor=corNatacao
        )
    )
  }
  //Seção:piscina(Dentro de Containers )
  SecaoTituloNatacao("Piscinas",corNatacao,Icons.Default.Pool)

  Column(modifier.padding(horizontal=16.dp)){
    CardLocalNatacao("Clube Aquatico Central","4.8 * 2.3km","Piscina Semiolimpica",corNatacao,onReservar)
    CardLocalNatacao("Academia AquaFit","4.5 * 3.1km", "Raia livre disponível",corNatacao,onReservar)
  }
  //Seção:Grupos(Dentro de Containers)
  SecaoTituloNatacao("Grupos de Treino",corNatacao,Icons.Default.Groups)
  
  Column(modifier=Modifier.padding(horizontal=16.dp)){
    CardGrupoNatacao("Nadadores Matinais","45 membros * 06:00","Iniciante * Manhã",corNatacao)
    CardGrupoNatacao("Competição Livre","28 membros * 19:00","Avançado * Noite",Color(0xFF009688))

    }
  }

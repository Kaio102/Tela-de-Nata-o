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
    // Container:Dicas (Estilo Image_23A3C3)
    SecaoTituloNatacao("Dicas Diárias",corNatacao,Icons.Default.Lightbulb)

    CardDicaNatacao(
        titulo="Respiração Correta",
        texto="Expire debaixo d'água e inspire rapidamente quando virar a cabeca para o lado.",
        corFundo=Color(0xFFC5CAE9)//Lilás conforme image_23a3c3.png 
    )
    Space(modifier=Modifier.height(12.dp))

    CardDicaNatacao(
        titulo-"Aquecimento",
        texto="Sempre faça 5-10 minutos de Aquecimento antes de começar o treino principal.",
        corFundo=Color(0xFFB2DFDB)//Ciano suave conforme image_23a3c3.png
    )
    Space(modifier=Modifier.height(30.dp))
      }
    }
  }
  // Componentes com containers modernos

@Composable
fun SecaoTituloNatacao(titulo:String,cor:Color,icone:androidx.compose.ui.graphics.vector.ImageVector){
    Row(modifier=Modifier.padding(16.dp),verticalAlignment=Alignment.CenterVertically){
        Icon(icone,null,tint=cor,modifier=Modifier.size(22.dp))
        Spacer(modifier=Modifier.width(8.dp))
        Text(titulo,fontSize=18.sp,fontWeight=FontWeight.ExtraBold,color=cor)
    }
}
@Composable
fub CardLocalNatacao(nome:String,info:String,status:String,cor:Color,onClick:()->Unit){
    Card(
        modifier=Modifier
        .fillMaxWidth()
        .padding(bottom=12.dp)
        .clickable{onClick()},
        colors=CardDefaults.cardColors(containerColor=Color.White),
        border=BorderStroke(1.dp,cor.copy(alpha=0.2f)),
        shape=RoundedCornerShape(16.dp),
        elevation=CardDefaults.cardElevation(2.dp)
    ){
        Row(modifier=Modifier.padding(16.dp),verticalAlignment=Alignment.CenterVertically){
            Surface(
                modifier=Modifier.size(55.dp),
                shape=RoundedCornerShape(12.dp),
                color=cor.copy(alpha=0.1f)
            ){
                Icon(Icons.Default.Pool,null,tint=cor,modifier=Modifier.padding(12.dp))
            }
            Column(modifier=Modifier.padding(Start=16.dp).weight(1f)){
                Text(nome,fontWeight=FontWeight.Bold,fontSize=16.sp)
                Text(info,fontSize=12.sp,color=Color.Gray)
                Text(status,fontSize=12.sp,color=cor,fontWeight=FontWeight.SemiBold)
            }
            Icon(Icons.Default.ArrowForwardlos,null,tint=Color.LightGray,modifier=Modifier.size(16.dp))
        }
    }
}
@Composable
fun CardGrupoNatacao(nome:String,membros:String,status:String,cor:Color){
    Card(
        modifier=Modifier
        .fillMaxWidth()
        .padding(bottom=10.dp),
        colors=CardDefaults.cardColors(containerColor=Color.White),
        shape=RoundedCornerShape(16.dp),
        elevation=CardDefaults.cardElevation(1.dp)
    ){
        Row(modifier=Modifier.padding(16.dp),verticalAlignment=Alignment.CenterVertically){
            Surface(modifier=Modifier.size(48.dp),shape=CircleShape,color=cor){
                Icon(Icons.Default.Groups,null,tint=Color.White,modifier=Modifier.padding(10.dp))
            }
            Column(modifier=Modifier.padding(start=16.dp).weight(1f)){
                Text(nome,fontWeight=FontWeight.Bold,fontSize=15.sp)
                Text(membros,fontSize=12.sp,color=Color.Gray)
                Text(status,fontSize=12.sp,color=cor,fontWeight=FontWeight.Bold)
            }
            Button(
                onClick={},
                colors=ButtonDefaults.buttonColors(containerColor=cor),
                shape=RoundedCornerShape(10.dp)           
            ){
                Text("Entrar",fontSize=12.sp,fontWeight=FontWeight.Bold)
            }
        }
    }
}
@Composable
fun CardDicaNatacao(titulo:String,texto:String,corFundo:Color){
    Card(
        modifier=Modifier
        .fillMaxWidth()
        .padding(horizontal=16.dp),
        colors=CardDefaults.cardColors(containerColor=corFundo),
        shape=RoundedCornerShape(16.dp)
    ){
        Row(modifier=Modifier.padding(20.dp),verticalAlignment=Alignment.CenterVertically){
            Icon(Icons.Default.Lightbulb,null,tint=Color(0xFF3F51B5))
            Spacer(modifier=Modifier.width(16.dp))
            Column{
                Text(titulo,fontWeight=FontWeight.Black,color=Color(0xFF303F9F),fontSize=15.sp)
                Text(texto,fontSize=13.sp,color=Color.DarkGray)
            }
        }
    }
}
@Preview(showSystemUi=true)
@Composable
fun PreviewNatacaoContainer(){
    TelaNatacao(onVoltar={},onReservar={})
}

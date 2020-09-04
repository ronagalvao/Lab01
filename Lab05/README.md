
# Web como Plataforma e Subcomponentes
*Lab de Componentização e Reúso de Software 29/08/2020*

## Tarefa 1

No link do Google Drive [modelo](https://docs.google.com/presentation/d/1M3eM98yVZDYqfIaVog8pRs8b7ckVjEwDBPQ-lJ_V18U/edit?usp=sharing) ou no diretório [resources/](resources/) você encontrará um modelo para resolver a tarefa:

Escolha um conjunto de componentes do laboratório passado e os represente na forma de componentes com sub-componentes.

## Tarefa 2

Crie uma conta no [Codepen](https://codepen.io/), copie o código do exemplo [React 03 - Componente Barra](https://codepen.io/santanche/pen/KKzmbwR) para a sua conta e construa um exemplo de componente adaptando o exemplo apresentado. Por se tratar de programação em JavaScript, podem ser feitas adaptações bastante simples.

Link para o projeto no Codepen: [React 03 - Componente Colors](https://codepen.io/ronagalvao/pen/MWyOpwJ)

> Código do componente:
>
**HTML**
~~~html
<div id="app"></div>  
~~~

**CSS**
~~~css
html, body{
  display: flex;
  justify-content: center;
}
section#RetColors{
  margion-top: 36px;
  padding-bottom: 36px;
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 500px;
}
~~~


**JavaScript**
~~~javascript
const colorArr = [
  "red",
  "yellow",
  "green",
  "orange"
];

class Colors extends React.Component {
  constructor(props){
    super(props);
    
    this.state = {
      color: "green"
    };
  }
  
  componentDidMount() {
    let colorPos = 0;
    setInterval(() => {
      if(colorArr.length - 1 > colorPos) {
        this.setState({
          color: colorArr[colorPos]
        }); 
        colorPos++
        } else {
        this.setState({
          color: colorArr[colorPos]
        }); 
        colorPos = 0;
        }
      }, 700);
   }
  
  toggleColor(){
    if(this.state.color === "green"){
      this.setState({
      color: "orange"
      });
    } else{
      this.setState({
      color: "green"
      });
    }
  }
  changeColor(event){
    this.setState({
      color: event.target.value
    });
  }
                  
  render() {
    console.log(this.state);
    const styleObj = {
        backgroundColor: this.state.color,
        border: 'solid'       
    };
      
    return(
      <section style={styleObj} id="RetColors">
        <h2 onClick={this.toggleColor.bind(this)}>{this.state.color}</h2>  
        <input value={this.state.color} onChange={this.changeColor.bind(this)}/>
      </section>
    );
  } 
}

ReactDOM.render(<Colors name="Ronaldo" />, document.getElementById("app"));
~~~


      getPosts () {
         axios({
            method: 'GET',
            url: 'http://127.0.0.1:3000/list/'
          }).then((res)=>{
            console.log("resGET1>>>", res)
            this.list = res.data
            console.log("resGET2>>>", this.list)
          })
      },
      createNewstoryList() {
        //validate vueContainer
        if (!this.vueContainer){
          alert("Please enter a vueContainer!");
          return
        }

        var self=this;
        const newId = Math.max.apply(null, this.list.map(t => t.id)) + 1;
        console.log("newId>>>", newId)
        axios.post('http://127.0.0.1:3000/list/', { id: newId, text: this.vueContainer, imgUrl: `${this.logo}`})
        .then((response) => {
          self.getPosts();
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
        
        
        this.vueContainer = '';
      },
      onDeleteItem(vueContainer){
       
        var self=this;
        axios({
          method: 'DELETE',
          url: 'http://127.0.0.1:3000/list/'+vueContainer.id,
          headers: { 'Content-Type': 'application/json' },
        }).then((res)=>{
            self.getPosts();
        });

        // this.list = this.list.filter(item => item !== vueContainer);
      }


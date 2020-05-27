//you need to use this onUpdate function inside your editor’s instance
  editor: new Editor({
    onUpdate: ({ getHTML }) => {
      const newPost = getHTML()
      //look for the letter i and change it
      if (newPost.match(/\s\i\s/g)) {
        const data = newPost.replace(/\s\i\s/g, ' I ')
        this.editor.setContent(data, true, { preserveWhitespace: true })
      }
      //look in each paragraph for the first letter not capitalized and change it
      if (newPost.match(/<p>[a-z]/g)) {
        const dataParse = newPost.split(/<p>(.*?)<\/p>/g)
        const strTrim = dataParse.filter(el => el.length)
        const strChange = strTrim.map(el => '<p>' + el.charAt(0).toUpperCase() + el.slice(1) + '</p>')
        const result = strChange.join(' ')
        this.editor.setContent(result, true, { preserveWhitespace: true })
      }
    },
  })


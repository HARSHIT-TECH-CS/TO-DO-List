#to do list
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

let todo = [];

function askCommand() {
  rl.question('\nEnter a command (add, list, remove, quit): ', (command) => {
    if (command === 'quit') {
      console.log('👋 Quitting the app...');
      rl.close();
    } else if (command === 'list') {
      console.log('\n📋 Your Tasks:');
      if (todo.length === 0) {
        console.log('No tasks yet.');
      } else {
        todo.forEach((task, index) => {
          console.log(`${index + 1}. ${task}`);
        });
      }
      askCommand();
    } else if (command === 'add') {
      rl.question('Enter the task to add: ', (task) => {
        todo.push(task);
        console.log(`✅ Added: ${task}`);
        askCommand();
      });
    } else if (command === 'remove') {
      rl.question('Enter the exact task to remove: ', (task) => {
        const index = todo.indexOf(task);
        if (index !== -1) {
          todo.splice(index, 1);
          console.log(`❌ Removed: ${task}`);
        } else {
          console.log('⚠ Task not found!');
        }
        askCommand();
      });
    } else {
      console.log('❓ Invalid command!');
      askCommand();
    }
  });
}

console.log('📝 Welcome to the Terminal To-Do App!');
askCommand();

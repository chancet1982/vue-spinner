<template lang="html">
	<div class="spinner">
		<button class="btn spinner-btn spinner-btn-down" :class="[{disabled:isStepDownDisabled}, {'hidden': !showButtons}, actualDirection]" @click="stepDown" :disabled="isStepDownDisabled">-</button>
		<input class="spinner-input" type="Number" name="" v-model="currentValue" :readonly="!inputEditable" step="{step}" min="min" max="max" :disabled="disabled" @blur="parseNumber"></input>
		<button class="btn spinner-btn spinner-btn-up" :class="[{disabled:isStepUpDisabled}, {'hidden': !showButtons}, actualDirection]" @click="stepUp" :disabled="isStepUpDisabled">+</button>
	</div>
</template>

<script>
export default {
	props: {
		initialValue: { //in place
			type: Number,
			required: false,
			default: 0,
		},
		step: { //in place
			type: Number,
			required: false,
			default: 1,
		},
		allowNegatives: { //in place
			type:Boolean,
			required: false,
			default: false,
		},
		inputEditable: { //In place
			type:Boolean,
			required: false,
			default: true,
		},
		showButtons: { //In place
			type:Boolean,
			required: false,
			default: true,
		},
		direction: {
			type:String,
			required: false,
			default: "horizontal",
		},
		min: { //in place (if false works)
			type: Number,
			required: false,
			default: this.min > 0 ? this.min : this.allowNegatives ? 0 : -999999,
		},
		max: { //in place (if false works)
			type: Number,
			required: false,
			default: this.max || 999999,
		},
		readonly: { //In place
			type:Boolean,
			required: false,
			default: false,
		},
		disabled: { //In place
			type:Boolean,
			required: false,
			default: false,
		},
		required: { //TODO should work with emitting some sort of state to parent component when valid
			type:Boolean,
			required: false,
			default: true,
		},
	},
	methods: {
		stepUp() {
			this.currentValue =this.currentValue + this.step;
			this.emitUpdatedAmount();
		},
		stepDown() {
			this.currentValue = this.currentValue - this.step;
			this.emitUpdatedAmount();
		},
		parseNumber(){
			this.currentValue = parseInt(this.currentValue, 10);
			this.emitUpdatedAmount();
		},
		emitUpdatedAmount(){
			const payload = {
				currentValue: this.currentValue
			};
			this.$emit("update-amount", payload);
		},
	},
	computed: {
		actualDirection(){
			 return this.direction === "vertical" ? "vertical" : "horizontal";
		},
		isStepUpDisabled() {
			return this.disabled ? true: (this.currentValue + this.step > this.max);
		},
		isStepDownDisabled() {
			return this.disabled ? true: (this.currentValue - this.step < this.min);
		},
	},
	data (){
		return {
			currentValue: this.initialValue > this.min ? this.initialValue : this.min,
		}
	},
}
//TODO add pattern validation on keydown based on regular expression to remove last char if not number
</script>

<style lang="scss" scoped>
.spinner {
	.btn {
		border:none;
		background:none;
		outline: none;
	}
	.spinner-btn{
		cursor: pointer;
		border-radius: 5px;
		display: inline-block;
		line-height: 32px;
		width: 32px;
		height: 32px;
		background-color: rgb(30, 180, 160);
		color: rgb(255, 255, 255);
		&:hover {
			background-color:rgb(40, 190, 190);
			box-shadow: 0 1px 2px 0 rgba(0,0,0,0.3);
		}
		&.disabled {
			background-color: rgb(230, 230, 230);
			color: #666;
			cursor: default;
		}
		&.hidden {
			display: none;
		}
		&.horizontal {
			//TODO finish styling
		}
		&.vertical {
			//TODO finish styling
		}
	}
	.spinner-input {
		width: auto;
		max-width: 100px;
		text-align: right;
		border: solid 1px #ddd;
		height: 32px;
		line-height: 32px;
	}
}

</style>
